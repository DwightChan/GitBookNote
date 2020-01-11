# KVO内部实现原理

#### **17. KVO内部实现原理？**

答：<br/>

KVO 的实现也依赖于 Objective-C 强大的 Runtime 。Apple 的文档有简单提到过 KVO 的实现：

> Automatic key-value observing is implemented using a technique called isa-swizzling... When an observer is registered for an attribute of an object the isa pointer of the observed object is modified, pointing to an intermediate class rather than at the true class ...

Apple 的文档真是一笔带过，唯一有用的信息也就是：被观察对象的 isa 指针会指向一个中间类，而不是原来真正的类。看来，Apple 并不希望过多暴露 KVO 的实现细节。不过，要是你用 runtime 提供的方法去深入挖掘，所有被掩盖的细节都会原形毕露。Mike Ash 早在 2009 年就做了这么个探究。

**简单概述下 KVO 的实现：**

当你观察一个对象时，一个新的类会动态被创建。这个类继承自该对象的原本的类，并重写了被观察属性的 setter 方法。自然，重写的 setter 方法会负责在调用原 setter 方法之前和之后，通知所有观察对象值的更改。最后把这个对象的 isa 指针 ( isa 指针告诉 Runtime 系统这个对象的类是什么 ) 指向这个新创建的子类，对象就神奇的变成了新创建的子类的实例。

原来，这个中间类，继承自原本的那个类。不仅如此，Apple 还重写了 -class 方法，企图欺骗我们这个类没有变，就是原本那个类。更具体的信息，去跑一下 Mike Ash 的那篇文章里的代码就能明白，这里就不再重复。

#### **18. 如何关闭默认的KVO的默认实现，并进入自定义的KVO实现？**

答：<br/>
如果没找到理想的，就自己动手做一个。既然我们对官方的 API 不太满意，又知道如何去实现一个 KVO，那就尝试自己动手写一个简易的 KVO 玩玩。

首先，我们创建 NSObject 的 Category，并在头文件中添加两个 API：<br/>

```objectivec
typedef void(^PGObservingBlock)(id observedObject, NSString *observedKey, id oldValue, id newValue);

@interface NSObject (KVO)

- (void)PG_addObserver:(NSObject *)observer
                forKey:(NSString *)key
             withBlock:(PGObservingBlock)block;

- (void)PG_removeObserver:(NSObject *)observer forKey:(NSString *)key;

@end
```

接下来，实现 PG_addObserver:forKey:withBlock: 方法。逻辑并不复杂：

① 检查对象的类有没有相应的 setter 方法。如果没有抛出异常；<br/>
② 检查对象 isa 指向的类是不是一个 KVO 类。如果不是，新建一个继承原来类的子类，并把 isa 指向这个新建的子类；<br/>
③ 检查对象的 KVO 类重写过没有这个 setter 方法。如果没有，添加重写的 setter 方法；<br/>
④ 添加这个观察者<br/>

```objectivec
- (void)PG_addObserver:(NSObject *)observer
                forKey:(NSString *)key
             withBlock:(PGObservingBlock)block
{
    // Step 1: Throw exception if its class or superclasses doesn't implement the setter
    SEL setterSelector = NSSelectorFromString(setterForGetter(key));
    Method setterMethod = class_getInstanceMethod([self class], setterSelector);
    if (!setterMethod) {
        // throw invalid argument exception
    }

    Class clazz = object_getClass(self);
    NSString *clazzName = NSStringFromClass(clazz);

    // Step 2: Make KVO class if this is first time adding observer and 
    //          its class is not an KVO class yet
    if (![clazzName hasPrefix:kPGKVOClassPrefix]) {
        clazz = [self makeKvoClassWithOriginalClassName:clazzName];
        object_setClass(self, clazz);
    }

    // Step 3: Add our kvo setter method if its class (not superclasses) 
    //          hasn't implemented the setter
    if (![self hasSelector:setterSelector]) {
        const char *types = method_getTypeEncoding(setterMethod);
        class_addMethod(clazz, setterSelector, (IMP)kvo_setter, types);
    }

    // Step 4: Add this observation info to saved observation objects
    PGObservationInfo *info = [[PGObservationInfo alloc] initWithObserver:observer Key:key block:block];
    NSMutableArray *observers = objectivec_getAssociatedObject(self, (__bridge const void *)(kPGKVOAssociatedObservers));
    if (!observers) {
        observers = [NSMutableArray array];
        objectivec_setAssociatedObject(self, (__bridge const void *)(kPGKVOAssociatedObservers), observers, objectivec_ASSOCIATION_RETAIN_NONATOMIC);
    }
    [observers addObject:info];
}
```
再来一步一步细看。

第一步里，先通过 setterForGetter() 方法获得相应的 setter 的名字（SEL）。也就是把 key 的首字母大写，然后前面加上 set 后面加上 :，这样 key 就变成了 setKey:。然后再用 class_getInstanceMethod 去获得 setKey: 的实现（Method）。如果没有，自然要抛出异常。

第二步，我们先看类名有没有我们定义的前缀。如果没有，我们就去创建新的子类，并通过 object_setClass() 修改 isa 指针。

```objectivec
- (Class)makeKvoClassWithOriginalClassName:(NSString *)originalClazzName
{
    NSString *kvoClazzName = [kPGKVOClassPrefix stringByAppendingString:originalClazzName];
    Class clazz = NSClassFromString(kvoClazzName);

    if (clazz) {
        return clazz;
    }

    // class doesn't exist yet, make it
    Class originalClazz = object_getClass(self);
    Class kvoClazz = objectivec_allocateClassPair(originalClazz, kvoClazzName.UTF8String, 0);

    // grab class method's signature so we can borrow it
    Method clazzMethod = class_getInstanceMethod(originalClazz, @selector(class));
    const char *types = method_getTypeEncoding(clazzMethod);
    class_addMethod(kvoClazz, @selector(class), (IMP)kvo_class, types);

    objectivec_registerClassPair(kvoClazz);

    return kvoClazz;
}
```

动态创建新的类需要用 objectivec/runtime.h 中定义的 objectivec_allocateClassPair() 函数。传一个父类，类名，然后额外的空间（通常为 0），它返回给你一个类。然后就给这个类添加方法，也可以添加变量。这里，我们只重写了 class 方法。哈哈，跟 Apple 一样，这时候我们也企图隐藏这个子类的存在。最后 objectivec_registerClassPair() 告诉 Runtime 这个类的存在。

第三步，重写 setter 方法。新的 setter 在调用原 setter 方法后，通知每个观察者（调用之前传入的 block ）：

```objectivec
static void kvo_setter(id self, SEL _cmd, id newValue)  
{
    NSString *setterName = NSStringFromSelector(_cmd);
    NSString *getterName = getterForSetter(setterName);

    if (!getterName) {
        // throw invalid argument exception
    }

    id oldValue = [self valueForKey:getterName];

    struct objectivec_super superclazz = {
        .receiver = self,
        .super_class = class_getSuperclass(object_getClass(self))
    };

    // cast our pointer so the compiler won't complain
    void (*objectivec_msgSendSuperCasted)(void *, SEL, id) = (void *)objectivec_msgSendSuper;

    // call super's setter, which is original class's setter method
    objectivec_msgSendSuperCasted(&superclazz, _cmd, newValue);

    // look up observers and call the blocks
    NSMutableArray *observers = objectivec_getAssociatedObject(self, (__bridge const void *)(kPGKVOAssociatedObservers));
    for (PGObservationInfo *each in observers) {
        if ([each.key isEqualToString:getterName]) {
            dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
                each.block(self, getterName, oldValue, newValue);
            });
        }
    }
}
```

细心的会发现我们对 objectivec_msgSendSuper 进行类型转换。在 Xcode 6 里，新的 LLVM 会对 objectivec_msgSendSuper 以及 objectivec_msgSend 做严格的类型检查，如果不做类型转换。Xcode 会抱怨有 too many arguments 的错误。（在 WWDC 2014 的视频 What new in LLVM 中有提到过这个问题。）

最后一步，把这个观察的相关信息存在 associatedObject 里。观察的相关信息（观察者，被观察的 key, 和传入的 block ）封装在 PGObservationInfo 类里。

```objectivec
@interface PGObservationInfo : NSObject

@property (nonatomic, weak) NSObject *observer;
@property (nonatomic, copy) NSString *key;
@property (nonatomic, copy) PGObservingBlock block;

@end
```