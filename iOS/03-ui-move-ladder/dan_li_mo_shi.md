# 单例模式
<br/>
##0. 本节知识点:
1. 基本概念
2. ARC实现单例
3. MRC实现单例
4. 单例实现注意点
5. 面试写简单单例
6. 通用版本单例(附详细代码)


---
<br/>

##1. 基本概念

- **概念**
    - 在程序运行过程，一个类只有一个实例
    - 即是创建多个相同类的对象, 都只有一个实例对象, 通过打印地址可以查看
    - 这份资源只需要创建初始化1次
- **作用**
    - 可以保证在程序运行过程，一个类只有一个实例，而且该实例易于供外界访问
    - 从而方便地控制了实例个数，并节约系统资源
- **使用场合**
    - 在整个应用程序中，共享一份资源（这份资源只需要创建初始化1次）
    - 举例：比如说登录控制器等等


---
<br/>


##2. ARC环境实现单例

- **实现单例步骤**
    - 新建一个类(继承 NSObject)
    - 控制内存分配，重写`-allocWithZone:`方法
        - `+(instancetype)alloc`内部会调用`-allocWithZone:`方法, 因此我们只需要重写 `-allocWithZone`方法即可
    - 创建一个全局的静态变量(`static`来修饰)
        - 
        - 如果只是普通全局变量在外界可以通过 extern 修饰引用, 也就可以在不同文件中修改变量的内容, 所以必须用 static 修饰, 变为内部全局变量
    - 使用 **GCD 的一次性函数**的方式来保证只分配一次
        - 或者使用加锁的方式来保证只分配一次
    - 为了方便外界访问，还应该提供一个类方法

    - 严谨起见: 重写`-copyWithZone:`和`- mutableCopyWithZone:`方法
        - `- (id)copy{}` 内部会调用`- copyWithZone:` 方法
        - `- (id)mutableCopy{}`内部会调用`- mutableCopyWithZone:` 方法
        - 注意：对象方法, 调用该方法说明对象已经存在了，所以直接返回即可


- **作用**
    - 方便外界访问
    - 表明这是一个单例


- **注意点**
    - 方法名称的命名规范：share+类名|share|defaule +类名|类名
    - 在实现中指出是直接使用Self还是类名
    - 在实现中指出是否还需要使用一次性代码和加锁<br/>

  
- **相关代码**

```objc
//提供一个static修饰的全局变量，强引用着已经实例化的单例对象实例
static CDHTools *_instance;

//类方法，返回一个单例对象
+(instancetype)shareTools
{
     //注意：这里建议使用self,而不是直接使用类名Tools（考虑继承）
    return [[self alloc]init];
}

//保证永远只分配一次存储空间
+(instancetype)allocWithZone:(struct _NSZone *)zone
{
//    // 加锁可以保证多线程时的数据安全 (但不常用, 加锁比较好性能)
//    @synchronized(self) {
//        if (_instance == nil) {
//            // 调用父类父类的方法分配存储空间
//            _instance = [super allocWithZone:zone];
//        }
//    }

    // 使用 GCD 的一次性代码创建模式 (常用)
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        _instance = [super allocWithZone:zone];
    });
    return _instance;
}

/*
1. mutableCopy 创建一个新的可变对象，并初始化为原对象的值，新对象的引用计数为 1；
2. copy 返回一个不可变对象。分两种情况：
  2.1 若原对象是不可变对象，那么返回原对象，并将其引用计数加 1 ；
  2.2 若原对象是可变对象，那么创建一个新的不可变对象，
      并初始化为原对象的值，新对象的引用计数为 1。
*/
//让代码更加的严谨
-(nonnull id)copyWithZone:(nullable NSZone *)zone
{
//    return [[self class] allocWithZone:zone];
    return _instance;
}

-(nonnull id)mutableCopyWithZone:(nullable NSZone *)zone
{
    return _instance;
}
```

---
<br/>

##3. MRC环境实现单例
- **实现单例步骤**
    - 新建一个类(继承 NSObject)
    - 控制内存分配，重写allocWithZone:方法
        - `+(instancetype)alloc`内部会调用`allocWithZone:`方法, 因此我们只需要重写 `allocWithZone`方法即可
    - 创建一个全局的静态变量(`static`来修饰)
        - 如果只是普通全局变量在外界可以通过 extern 修饰引用, 也就可以在不同文件中修改变量的内容, 所以必须用 static 修饰, 变为内部全局变量
    - 使用 **GCD 的一次性函数**的方式来保证只分配一次
        - 或者使用加锁的方式来保证只分配一次
    - 为了方便外界访问，还应该提供一个类方法

    - 严谨起见: 重写`-copyWithZone:`和`- mutableCopyWithZone:`方法
        - `- (id)copy{}` 内部会调用`- copyWithZone:` 方法
        - `- (id)mutableCopy{}`内部会调用`- mutableCopyWithZone:` 方法
        - 注意：对象方法, 调用该方法说明对象已经存在了，所以直接返回即可



- **配置MRC环境知识**
    - ARC不需要手动回收内存, Xcode 编译的时候已经帮我们做了内存回收, 注意: ARC 不是垃圾回收机制，是编译器特性
    - 配置为MRC环境：build setting ->搜索automatic ref->修改为NO
    - 运行程序，报错。这个时候先在单例类里面添加一个dealloc方法，打印方法的名称。打开僵尸对象检测。查看为什么会报错。
           
    ![设置MRC环境](../images/多线程/设置MRC环境.png)

- **比 ARC 项目中多写下面几个方法 **
    - 重写`- release`方法: 在方法中什么不做
        - 对于其他的对象可能每alloc init一次，就release,new一次就release一次,
        - 如果单例被释放掉就没办法在共享资源了, 并指出但如果不断地创建与释放那也就不是单例了
        -  因此单例不需要手动释放, 单例被创建之后直到程序退出才被释放, 否则可能导致多次释放<br/><br/>

    - 重写`- retain`方法: 返回对象本身.
        - 别人有可能会调用retain方法，让引用计数器加1，这样可能会产生内存泄露, 因此每次值返回对象本身即可<br/><br/>
    - 重写retainCount方法: 
        - 为了方便程序员之间沟通，提高代码的可阅读性，推荐重写retainCount方法，返回一个约定的值, 一般是最大值`return MAXFLOAT`

```objc
// 在 MRC 项目中单例的代码还要比 ARC 的代码多出下面的代码
#if __has_feature(objc_arc)
// 在 ARC 环境就什么都不做使用系统默认的
#else
// MRC
- (oneway void)release{
    // 什么也不做
}
- (instancetype)retain{
    // 直接返回对象本身
    return _instance;
}
- (NSUInteger)retainCount{
    // 程序员的惯用做法, 单例对象一般都是直接返回一个最大的数
    return MAXFLOAT;
}
```

---

<br/>
##4. 单例实现注意点

- **问题: **一个项目中可能有很多的工具类，如果有很多的工具类都需要实现单例，应该怎么处理？
- **解决方案**
    - **单例不可以通过继承**;
        - 最直接的做法是采用继承,但该方法**不可行**, 如果使用继承还是只会创建父类单例, 
        - 如果重写了子类单例的类方法和对象方法, 则要需要全部重写才行, 因此单例不能通过继承<br/><br/>
    - **采用宏**
        - 单例模式（通用）:如果多个类都要实现单例模式，那么实现代码几乎是一模一样的
        - 宏实现单例
            - singleH
            - singleM
            - 使用连接符连接多行代码<br/><br/>
        - 带参数的宏
            - 使用带参数的宏主要解决类方法名称的问题
            - 条件编译不能写在宏里面<br/><br/>
    - **通用版单例详细代码**(见本页最后一个知识点: 6. 通用版单例)


---
<br/>
##5. 面试写简单单例
- **是什么保证了单例的生命周期是整个程序**
    - static 关键字修饰的全局静态变量
- **哪些地方可以用到单例**
    - 在回答的时候结合单例的特性，单例虽然强大但是不要滥用

```objc
//单例模式的简写方式
//类方法，返回一个单例对象
//优点:代码简单
//缺点:单例实现并不彻底
+(instancetype)shareXMGDownloadTool
{
    static XMGDownloadTool *_instance;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        _instance = [[self alloc]init];
    });
    
    return _instance;
}
```


--- 
<br/>


##6. 通用版本

>开发人员可能会在ARC和MRC环境切换，如何做到不管是ARC还是MRC的环境我们的单例模式都可以使用
使用宏来判断当前环境，结合条件编译解决上面的问题

- **问01: 写一份单例代码在ARC和MRC环境下都适用？**
    - 答：可以使用条件编译来判断当前项目环境是ARC还是MRC<br/><br/>
- **问02: 条件编译的代码？**

```objc
#if __has_feature(objc_arc)
//如果是ARC，那么就执行这里的代码1
#else
//如果不是ARC，那么就执行这里的代码2
#endif
```

- **问03：在项目里面往往需要实现很多的单例，比如下载、网络请求、音乐播放等等，单例是否可以用继承？**
    - 答：单例是不可以用继承的，如果想一次写就，四处使用，那么使用带参数的宏定义.

- **使用带参数的宏完成通用版单例模式代码**
    - 注意:条件编译的代码不能包含在宏定义里面
    - 宏定义的代码只需要写一次就好，之后直接拖到项目中用就即可

```objc
//
//  Single.h
//  day02-05-通用版单例
//
//  Created by Dwight on 16/6/18.
//  Copyright © 2016年 Dwight. All rights reserved.
//


#define SingleH(name) +(instancetype)share##name;

#if __has_feature(objc_arc)
// ARC
#define SingleM(name) static id _instance;\
+ (instancetype)allocWithZone:(struct _NSZone *)zone{\
static dispatch_once_t onceToken;\
dispatch_once(&onceToken, ^{\
_instance = [super allocWithZone:zone];\
});\
return _instance;\
}\
\
+ (instancetype)share##name{\
return [[self alloc]init];\
}\
\
- (id)copyWithZone:(struct _NSZone *)zone{\
return _instance;\
}\
\
- (id)mutableCopyWithZone:(struct _NSZone *)zone{\
return  _instance;\
}\

#else
// MRC
#define  SingleM(name) static id _instance;\
+ (instancetype)allocWithZone:(struct _NSZone *)zone{\
static dispatch_once_t onceToken;\
dispatch_once(&onceToken, ^{\
_instance = [super allocWithZone:zone];\
});\
return _instance;\
}\
\
+ (instancetype)share##name{\
return [[self alloc]init];\
}\
- (id)copyWithZone:(struct _NSZone *)zone{\
return _instance;\
}\
- (id)mutableCopyWithZone:(struct _NSZone *)zone{\
return  _instance;\
}\
\
- (oneway void)release{\
}\
- (instancetype)retain{\
return _instance;\
}\
- (NSUInteger)retainCount{\
return MAXFLOAT;\
}\

#endif

```

---