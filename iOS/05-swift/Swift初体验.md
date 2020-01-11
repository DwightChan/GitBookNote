#Swift初体验

---

![Swif初体验](http://upload-images.jianshu.io/upload_images/2173180-a56cf4fc073bf126.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- **一般学习 Swift 都是在 Playground 中学习**

- **Playground是什么?**
	- 从Xcode6开始出现(Swift开始出现)
	- 翻译为:操场/游乐场
	- 对于学习Swift基本语法非常方便
		- 所见即所得(快速查看结果)
		- 语法特性发生改变时,可以快速查看.


- **Swift最基本的语法变化**
	- 导入框架 import UIKit
	- 定义标识符时，必须声明该标识符是变量还是常量
		- 声明标识符的格式:变量/常量关键字 名称 : 数据类型


- **语句结束时不需要加分号`(;)`**
    - 如果同一行有多个语句,则依然需要加
	- 但是不建议一行多条语句



<br />

<br />

---

- **学习swift第一步打印Hello World**
    - 一条swift语句结束时是不用加分号`(;)`的, 编译器自动会帮我们写上, 当然如果自己写了分号`(;)`也没错
    - 注意: 如果是多条语句写在同一行, 则必须用分号`(;)`隔开

```swift
print("Hello World")
```



- **创建对象**
	* **OC:**     alloc initWithXXX 方法
	* **Swift:**  (xxx:)


- **调用方法**
	* **OC:**     [UIColor redColor];
	* **Swift:**   
        *  ~~UIColor.redColor() // swift 2.3~~ 
        * UIColor.red // swift 3.1

- **枚举**
	* **OC: **     UIButtonTypeContactAdd
	* **Swift:**   
        * ~~UIButtonType.ContactAdd // swift 2.3~~
        * UIButtonType.contactAdd // swift 3.1


```swift 
//[[UIView alloc] init];
//[[UIView alloc] initWithFrame: ];
//let view = UIView()

let view = UIView(frame:CGRect(x: 0, y: 0, width: 100, height: 100))
// swift 2.3
// view.backgroundColor = UIColor.redColor()
// swift 3.1
view.backgroundColor = UIColor.red

// swift 2.3
// let btn = UIButton(type: UIButtonType.ContactAdd)
// swift 3.1
let btn = UIButton(type: UIButtonType.contactAdd)
btn.center = view.center
view.addSubview(btn)
```