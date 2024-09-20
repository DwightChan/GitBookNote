# 应用程序的程动原理

- **应用程序启动原理: 程序完整启动流程**
    - 1.执行main函数
    - 2.执行UIApplicationMain函数.
    - 3.创建UIApplication对象,并设置UIApplicationMain对象的代理.
        - UIApplicationMain函数的第三个参数就是UIApplication的名称,如果指定为nil,它会默认为UIApplication.
        - UIApplication的第四个参数为UIApplication的代理.
    - 4.开启一个主运行循环(死循环).保证应用程序不退出.
    - 5.加载info.plist.加载配置文件.判断一下info.plist文件当中与 key 为 Main storyboard file base name 对应的 value 是否有值, 这个值就是对应的后缀名为 .storyboard 的文件名称
        - 如果有就去加载 这个 key 对应的 value 的 storyboard文件, 
        - 如果没有,那么应用程序也会加载完毕.但是就不会有显示窗口
        - 这时候显示窗口就要在 UIApplication 的加载完毕时会调用的代理方法`- (BOOL)application:didFinishLaunchingWithOptions:`中创建, 同时注意要给窗口添加一个根控制器

```objc
//
//  main.m
//  day05-10-掌握-NSURLSession文件下载(dataTask·开始暂停取消继续等常见操作)
//
//  Created by Dwight on 16/6/24.
//  Copyright © 2016年 Dwight. All rights reserved.
//

#import <UIKit/UIKit.h>
#import "AppDelegate.h"

int main(int argc, char * argv[]) {
    @autoreleasepool {
        return UIApplicationMain(argc, argv, nil, NSStringFromClass([AppDelegate class]));
        // 第三个参数:UIApplication类名或者子类的名称 nil == @"UIApplication"
        // 第四个参数:UIApplication的代理的代理名称
        //        NSStringFromClass:把类名转化字符串
        //        NSStringFromClass:好处:1.有提示功能 2.避免输入错误
        //        return UIApplicationMain(argc, argv, NSStringFromClass([UIApplication class]), NSStringFromClass([AppDelegate class]));
        //        return UIApplicationMain(argc, argv,@"UIApplication", NSStringFromClass([AppDelegate class]));
    }
}
```