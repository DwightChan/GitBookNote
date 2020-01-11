# 08-UIWindow

```objc
   // 1. 创建窗口
    self.window = [[UIWindow alloc]initWithFrame:[UIScreen mainScreen].bounds];
    
    // 2. 设置窗口根控制器
    UIViewController *vc = [[UIViewController alloc]init];
    vc.view.backgroundColor = [UIColor redColor];
    // 一个窗口必须得 有根控制器
    self.window.rootViewController = vc;
    
    // 3. 显示窗口
    [self.window makeKeyAndVisible];

```