# 定位-Location


---


###1. iOS7实现定位功能
- 导入框架

```swift
import CoreLocation
```

- 创建运动管理者对象
    - 注意: 不能被释放, 要用强引用

```swift
// 定义一个定位管理者的属性, 强引用避免被释放
// 可以写成闭包的形式
private lazy var manager: CLLocationManager = CLLocationManager()
```

- 设置代理

```swift
// 2.设置代理
manager.delegate = self
```

```swift
// 将上面的写成闭包
lazy var manager : CLLocationManager = {
    let manager = CLLocationManager()
    manager.delegate = self
    return manager
}()
```

- 开启定位功能

```swift
manager.startUpdatingLocation()
```

- 在`CLLocationManagerDelegate`的代理方法中获取用户位置信息

```swift
// MARK : - 定位的代理方法
extension ViewController : CLLocationManagerDelegate {
    func locationManager(manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        print("每次请求到位置信息,都会调用这个代理方法")
    }
}
```

###2. 使用位置管理者进行定位补充:

- 如果想要使用位置管理者来开始实现某一个功能 :
    - 开启功能: start
    - 停止这个功能 : stop
- 一旦调用了startUpdatingLocation() 这个方法,就会不断的获取用户的位置信息
- 在 iOS6.0之后,如果想要获取用户的隐私(照片,通信),系统会主动弹框让用户授权, 一旦用户选则了don't allow 意味着再也无法获取用户的位置信息.除非用户到设置界面,设置允许你的app来获取当前的位置


- 如果希望给用户一个描述: info.plist 中配置 ,  配置Privacy - Location Usage Description 来说明定位目的

![Privacy - Location Usage Description.png](http://upload-images.jianshu.io/upload_images/2173180-a39354858169456e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###3. 实现后台定位

- **条件:**
    - 在前台基础上,勾选后台模式location updates或者直接info.plist文件,添加Required background modes(两者实现同一个操作)

- **操作: **
    - Capabilities -> Background Models -> 选中Location updates 打钩

![开启后台定位-图1.png](http://upload-images.jianshu.io/upload_images/2173180-076f28dfc861331a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- info.plist操作: 添加Required background modes-> App registers for location updates

![开启后台定位-图2.png](http://upload-images.jianshu.io/upload_images/2173180-91fa87fd0e22e75d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


#####4. 定位不到, 对应的代理方法不执行

- **解决:**
    - 首先,检查运行的模拟器是否是iOS8.0之前的系统版本
    - 其次,检查模拟器是否设置位置数据
    - 第三,确保代码无问题(一般都是代理没有设置,或者位置管理器对象是局部变量)
    - 第四,模拟器BUG, 请将模拟器位置设为None, 然后再次设置数据; 或者,重置模拟器













---

