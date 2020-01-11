# 位移枚举

<br/>
##1. 常见的几种枚举形式
```objc
//枚举一
typedef enum{
    XMGDemoTypeTop,
    XMGDemoTypeBottom,
}XMGDemoType;
```
```objc
//枚举二
typedef NS_ENUM(NSInteger,XMGType){
    XMGTypeTop,
    XMGTypeBottom,
};
```
```objc
//枚举三：位移枚举
typedef NS_OPTIONS(NSInteger, XMGActionType){
    XMGActionTypeTop = 1<<0,
    XMGActionTypeBottom = 1<<1,
    XMGActionTypeLeft = 1<<2,
    XMGActionTypeRight = 1 <<3,
};
```

---
<br/>
##2. 位移枚举相关说明
- **特点**：通过使用位移枚举可以实现一个参数实现传递多个操作
- **原理**：按位与只要有0则为0，按位或只要有1则为1
- **技巧**：如果位移枚举的第一个选项为0，那么在传递参数的时候默认可以传0，传0性能最优，不做额外的操作


---
<br/>