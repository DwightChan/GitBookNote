# 新特性

* 新特性是现在很多应用程序中包含的功能，主要用于在系统升级后，用户第一次进入系统时获知新升级的功能

## 课程目标

* UICollectionView 使用
* `根视图控制器` 切换

## 新特性功能

### 准备文件

* 将新特性图片素材拖拽到 Images.xcsets 中
* 建立 `NewFeature` 目录
* 新建 `NewFeatureViewController.swift` 继承自 `UICollectionViewController`
* 在 `NewFeatureViewController.swift` 的末尾添加如下代码：

### 代码实现

* 修改 `AppDelegate` 的根视图控制器

```swift
window?.rootViewController = NewFeatureViewController()
```

> 运行测试，崩溃！

* 原因：实例化 `CollectionViewController` 时必须指定布局参数

* 实现 `init()` 简化外部调用

```swift
/// 布局属性
let layout = UICollectionViewFlowLayout()

init() {
    super.init(collectionViewLayout: layout)
}

required init(coder aDecoder: NSCoder) {
    fatalError("init(coder:) has not been implemented")
}
```

* 定义 NewFeatureCell

```swift
class NewFeatureCell: UICollectionViewCell {

    private lazy var iconView: UIImageView = {
        return UIImageView()
    }()

    var imageIndex: Int = 0 {
        didSet {
            iconView.image = UIImage(named: "new_feature_\(imageIndex + 1)")
        }
    }

    override init(frame: CGRect) {
        super.init(frame: frame)

        addSubview(iconView)
    }

    required init(coder aDecoder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    override func layoutSubviews() {
        super.layoutSubviews()

        print(__FUNCTION__)

        iconView.frame = bounds
    }
}
```

* 注册可重用 Cell

```swift
override func viewDidLoad() {
    super.viewDidLoad()

    // 注册可重用 Cell
    self.collectionView!.registerClass(NewFeatureCell.self, forCellWithReuseIdentifier: reuseIdentifier)
}
```

> 运行测试，需要设置布局属性

* 设置布局属性

```swift
override func viewWillAppear(animated: Bool) {
    super.viewWillAppear(animated)

    // 设置布局
    layout.itemSize = view.bounds.size
    layout.minimumInteritemSpacing = 0
    layout.minimumLineSpacing = 0
    layout.scrollDirection = UICollectionViewScrollDirection.Horizontal

    self.collectionView?.pagingEnabled = true
    self.collectionView?.showsHorizontalScrollIndicator = false
    self.collectionView?.bounces = false
}
```

* 定义按钮

```swift
private lazy var startButton: UIButton = {
    let btn = UIButton()
    btn.setTitle("开始体验", forState: UIControlState.Normal)
    btn.setBackgroundImage(UIImage(named: "new_feature_finish_button"), forState: UIControlState.Normal)
    btn.setBackgroundImage(UIImage(named: "new_feature_finish_button_highlighted"), forState: UIControlState.Highlighted)

    return btn
}()
```

* 设置按钮布局

```swift
// 自动布局
iconView.translatesAutoresizingMaskIntoConstraints = false
addConstraints(NSLayoutConstraint.constraintsWithVisualFormat("H:|[subView]|", options: NSLayoutFormatOptions.AlignAllBaseline, metrics: nil, views: ["subView": iconView]))
addConstraints(NSLayoutConstraint.constraintsWithVisualFormat("V:|[subView]|", options: NSLayoutFormatOptions.AlignAllBaseline, metrics: nil, views: ["subView": iconView]))

startButton.translatesAutoresizingMaskIntoConstraints = false
addConstraint(NSLayoutConstraint(item: startButton, attribute: NSLayoutAttribute.CenterX, relatedBy: NSLayoutRelation.Equal, toItem: self, attribute: NSLayoutAttribute.CenterX, multiplier: 1.0, constant: 0))
addConstraint(NSLayoutConstraint(item: startButton, attribute: NSLayoutAttribute.Bottom, relatedBy: NSLayoutRelation.Equal, toItem: self, attribute: NSLayoutAttribute.Bottom, multiplier: 1.0, constant: -200))
```

* 添加动画

```swift

```


### 动画显示 `开始体验` 按钮

* 在 `NewFeatureCell` 中添加 `showStartButton` 函数

```swift
///  动画显示按钮
func showStartButton() {
    startButton.hidden = false
    startButton.transform = CGAffineTransformMakeScale(0, 0)
    startButton.userInteractionEnabled = false

    UIView.animateWithDuration(0.5, delay: 0, usingSpringWithDamping: 0.5, initialSpringVelocity: 5.0, options: UIViewAnimationOptions(rawValue: 0), animations: {
        self.startButton.transform = CGAffineTransformIdentity
        }, completion: { _ in
            self.startButton.userInteractionEnabled = true
    })
}
```

* 在 `collectionView` 的 `完成显示Cell` 代理方法中添加以下代码：

```swift
// 参数 cell, indexPath 是前一个 cell 和 indexPath
override func collectionView(collectionView: UICollectionView, didEndDisplayingCell cell: UICollectionViewCell, forItemAtIndexPath indexPath: NSIndexPath) {

    // 取出当前显示的 indexPath
    let indexPath = collectionView.indexPathsForVisibleItems().last!
    if indexPath.item == imageCount - 1 {

        let cell = collectionView.cellForItemAtIndexPath(indexPath) as! NewFeatureCell
        cell.showStartButton()
    }
}
```

> 注意：参数中的 `cell` & `indexPath` 是之前消失的 `cell`，而不是当前显示的 `cell` 的

### 隐藏状态栏

```swift
override func prefersStatusBarHidden() -> Bool {
    return true
}
```
