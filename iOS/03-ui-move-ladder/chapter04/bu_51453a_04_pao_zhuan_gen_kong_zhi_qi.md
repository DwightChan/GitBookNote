# 补充: 04 抛砖跟控制器

- 这里要说的是在 storyboard 中的**初始化箭头**
    > 当代码执行到下面这行语句的时候就会将 `Main.storyboard`文件中的初始化箭头抛给了`Main.storyboard`文件中 `lyu_tabBarVc`标识的控制器    
    > **注意: **这里前后两个控制器都在`Main.storyboard`文件中

```objc
// 抛砖跟控制器:
[UIApplication sharedApplication].keyWindow.rootViewController = [[UIStoryboardstoryboardWithName:@"Main"bundle:nil] instantiateViewControllerWithIdentifier: @"lyu_tabBarVc"];//抛砖跟控制器
```