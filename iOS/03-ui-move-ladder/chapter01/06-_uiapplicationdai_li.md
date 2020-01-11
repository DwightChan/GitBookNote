# 06- UIApplication代理
Make by:弓_虽_子   
MenderBy: 德豪   

>所有的移动操作系统都有个致命的缺点：app很容易受到打扰。
比如一个来电或者锁屏会导致app进入后台甚至被终止
还有很多其它类似的情况会导致app受到干扰，在app受到干扰时，会产生一些系统事件，
这时UIApplication会通知它的delegate对象，让delegate代理来处理这些系统事件

##delegate可处理的事件包括：
- 应用程序的生命周期事件(如程序启动和关闭)
- 系统事件(如来电)
- 内存警告
- ...


- UIApplication会在程序一启动时候创建一个遵守UIApplicationDelegate协议的代理.
- 这个就是我们程序一创建时的AppDelegate类.AppDelegate就是遵守了UIApplicationDelegate协议.
- 在这个类中定义很多监听系统事件的方法.同时也定义了一些应用程序的生命周期方法.

##主要方法有:

- 应用程序的生命周期
- 应用程序启动完成的时候调用

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
NSLog(@"%s",__func__);
return YES;
}
```

- 当我们应用程序即将失去焦点的时候调用

```objc
- (void)applicationWillResignActive:(UIApplication *)application {
NSLog(@"%s",__func__);
}
```

- 当我们应用程序完全进入后台的时候调用
- (void)applicationDidEnterBackground:(UIApplication *)application{
NSLog(@"%s",__func__);
}

当我们应用程序即将进入前台的时候调用
- (void)applicationWillEnterForeground:(UIApplication *)application {
          NSLog(@"%s",__func__);
}

当我们应用程序完全获取焦点的时候调用
只有当一个应用程序完全获取到焦点,才能与用户交互.
- (void)applicationDidBecomeActive:(UIApplication *)application {
          NSLog(@"%s",__func__);
}

当我们应用程序即将关闭的时候调用
- (void)applicationWillTerminate:(UIApplication *)application {
          NSLog(@"%s",__func__);
}
