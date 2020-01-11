#基本数据类型

---

###1. Swift类型的介绍

- Swift中的数据类型也有:整型/浮点型/对象类型/结构体类型等等
- 先了解整型和浮点型
- **整型**
    - 有符号
        - Int8 : 有符号8位整型
        - Int16 : 有符号16位整型
        - Int32 : 有符号32位整型
        - Int64 : 有符号64位整型
        - Int : 和平台相关(默认,相当于OC的NSInteger)
    - 无符号
        - UInt8 : 无符号8位整型
        - UInt16 : 无符号16位整型
        - UInt32 : 无符号32位整型
        - UInt64 : 无符号64位整型
        - UInt : 和平台相关(常用,相当于OC的NSUInteger)(默认)
- **浮点型**
    - Float : 32位浮点型
    - Double : 64浮点型(默认)

```swift
// 定义一个Int类型的变量m,并且赋值为10
var m : Int = 10
// 定义一个Double类型的常量n,并且赋值为3.14
let n : Double = 3.14
```

- Swift是类型安全的语言, 如果取值错误会直接报错, 而OC不会
```swift
//取值不对
//OC:unsigned int intValue = -10; 不会报错
var intValue8: UInt = -10 // swift会报错
// negative integer '-10' overflows when stored into unsigned type 'UInt'
//溢出:
//int intValue = INT_MAX + 1; //OC:不会报错
//var intValue9 :UInt = UInt.max + 1 //Swift:会报错
```

---


###2. Swift中的类型推导

- Swift是强类型的语言
- Swift中任何一个标识符都有明确的类型
- **注意:**
    - 如果定义一个标识符时有直接进行赋值,那么标识符后面的类型可以省略.
    - 因为Swift有类型推导,会自动根据后面的赋值来决定前面的标识符的数据类型
- 可以通过option+鼠标左键来查看数据类型推导

![数据类型推导.png](http://upload-images.jianshu.io/upload_images/2173180-75dec48a124e929c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```swift
// 定义变量时没有指定明确的类型,但是因为赋值给i一个20.20为整型.因此i为整型
var i = 20
// 错误写法:如果之后赋值给i一个浮点型数值,则会报错
// i = 30.5

// 正确写法
var j = 3.33
j = 6.66
```

---

###3. Swift中基本运算

- Swift中在进行基本运算时必须保证类型一致,否则会出错
    - 相同类型之间才可以进行运算
    - 因为Swift中没有隐式转换
- 数据类型的转化
    - Int类型转成Double类型:Double(标识符)
    - Double类型转成Int类型:Int(标识符)

```swift
let a = 10
let b = 3.14

// 错误写法
// let c = a + b
// let c = a * b

// 正确写法
let c = Double(a) + b
let d = a + Int(b)
```

- Swift:不具有隐式类型转换
```objectivec`
// 数据类型的相互赋值(隐式类型转换)
//OC可以隐式类型转换
//int intValue = 10;
//double doubleValue = intValue;
```
```swift
// 在Swift中“值永远不会被隐式转换为其他类型”(OC中可以隐式类型转换)

//以下语句会报错
var intValue10 :Int = 10
//var doubleValue11 :Double = intValue

//数据类型转换
//Swift不允许隐式类型转换, 但可以使用显示类型转换(强制类型转换)
//OC写法
//int intValue = 10;
//double doubleValue = (double)intValue;

//Swift写法:
var intValue12 :Int = 10
var doubleValue:Double
doubleValue = Double(intValue)
//注意:Double()并不会修改intValue的值
//而是通过intValue的值生成一个临时的值赋值给doubleValue
print(intValue)
print(doubleValue)


var willOverflow = UInt8.max
// willOverflow 等于UInt8的最大整数 255
willOverflow = willOverflow &+ 1
// 这时候 willOverflow 等于 0

```

---