# 抽取展现处理代码

## 目标

* 将展现处理代码从视图控制器中分离，以便于复用

## 代码实现

### 新建 `PopoverAnimator`

* 新建 `PopoverAnimator` 继承自 `NSOjbect`
* 让 `PopoverAnimator` 遵守 `UIViewControllerTransitioningDelegate` 和 `UIViewControllerAnimatedTransitioning`

```swift
class PopoverAnimator: NSObject, UIViewControllerTransitioningDelegate, UIViewControllerAnimatedTransitioning {

}
```

* 复制 `HomeTableViewController` 中的对应代码
* 增加 `presentedFrame` 属性

```swift
/// 展现位置
var presentedFrame: CGRect = CGRectZero
```

### 调整 `HomeTableViewController` 代码

* 删除原有协议相关代码
* 定义动画代理对象

```swift
///  转场动画代理
let popoverAnimatorDelegate = PopoverAnimator()
```

* 设置转场动画代理，由 `self` 改为 `popoverAnimatorDelegate`

```swift
if segue.identifier == "home2Firend" {
    titleButton.selected = true

    let vc = segue.destinationViewController as! PopoverViewController
    vc.transitioningDelegate = popoverAnimatorDelegate

    let w: CGFloat = 200
    let x = (self.view.bounds.size.width - w) * 0.5
    popoverAnimatorDelegate.presentedFrame =  CGRectMake(x, 56, w, 250)

    vc.modalPresentationStyle = UIModalPresentationStyle.Custom
}
```

> 运行测试！
