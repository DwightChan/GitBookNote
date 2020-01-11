# 补充: 状态栏和悬浮 Window

- **window 是有分等级的**
    - 级别越高的window越显示在上面, 
    - 级别相等的window,后面显示的window显示在上面; 


- **等级划分:**`UIWindowLevelNormal` < `UIWindowLevelStatusBar` < `UIWindowLevelAlert`


- **注意:** 状态栏是一个 Window 不是手机屏主显示 Window 的子控件两者是不是同级关系, 
    - 状态栏 window 是 UIWindowLevelStatusBar 级别,
    - 手机主屏 window 是 UIWindowLevelNormal 级别


- **手动添加window**
     - 注意: 如果添加在原有的状态栏的上面, 会挡住原有状态栏的一些特有的功能,
     - 注意: 如果不给自定义的 window 添加跟控制器, 则这个 window 是不能跟随屏幕旋转
     - 注意: 状态栏的显示颜色是由最顶层状态栏的跟控制器的状态栏样式的方法控制

  ```objc
  // 注意: 这个自己创建的 window 
  dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(0.1 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{

      self.topWindow = [[UIWindow alloc] init];
  //        self.topWindow.frame = application.statusBarFrame;
      self.topWindow.frame = CGRectMake(280, 500, 80, 80);
      self.topWindow.backgroundColor = [UIColor redColor];
      self.topWindow.windowLevel = UIWindowLevelAlert;
      self.topWindow.hidden = NO;
      [self.topWindow addGestureRecognizer:[[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(click)]];
  });
  ```


- **保留状态栏原有的功能的方法**
     - 在 AppDelegate.m 文件中实现下面的方法,
     - 注意: 处理掉超出状态栏以外的范围不接受点击事件

  ```objc
  @implementation AppDelegate
  /**  可以在这个AppDelegate方法中监听到状态栏的点击 */
  - (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{
      // 处理超出状态栏范围的点击事件响应
      if ([touches.anyObject locationInView:nil].y > 20) return;

      CDHLog(@"点击了状态栏")
  }
  ```