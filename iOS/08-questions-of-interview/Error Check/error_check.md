# Error Check 纠错

---

### 你是否接触过 OC 中的反射机制? 简单聊一下概念和使用

- class 反射
    - 通过类名的字符串形式实例化对象
    - 将类名变为字符串

- SEL 反射
    - 通过方法的字符串形式实例化方法
    - 将方法变成字符串

```objectivec
    /// class 反射
    //通过类名的字符串形式实例化对象
    Class class NSClassFromString(@"Student"); 
    Student *stu = [[class alloc ]init];
    //将类名变为字符串
    Class class = [Student class]; 
    NSString *className = NSStringFromClass(class);
    
    /// SEL 反射
    //通过方法的字符串形式实例化方法
    SEL selector = NSSelectorFromClass(@"setName");  
    [stu performSelector:selector withObject:@"Mike"];
    //将方法变成字符串
    NSStringFomrSelector(@selector(setName:));
```