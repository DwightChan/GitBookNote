# 补充01: 新特性界面


- 获取版本号
- 通过版本号判断是否是新版本
- 如果是新版本,显示新界面特性
- 如果不是,则不显示新界面特性

- **例如:**



- 创建两个类: 分别是: 主界面/新特性界面
- 在 AppDelegate.m 文件中创建界面....

```objc
#import "AppDelegate.h"
#import "XMGMainVc.h"
#import "XMGNewFeatureVc.h"

@interface AppDelegate ()

@end
```

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
//    1.创建window
    self.window = [[UIWindow alloc]initWithFrame:[UIScreen mainScreen].bounds];
//    2.获取当前的版本号
    NSString *curVersion = [NSBundle mainBundle].infoDictionary[@"CFBundleShortVersionString"];
//    2.1获取上一次的版本号
    NSString *lastVersion = [[NSUserDefaults standardUserDefaults]objectForKey:@"version"];
    if ([curVersion isEqualToString:lastVersion]) {//设置根控制器为主控制器
        
        XMGMainVc *mainVc = [[XMGMainVc alloc]init];
        self.window.rootViewController = mainVc;
    }else{//表示当前版本和上一次版本不一样,记录版本号,设置根控制器为新特性控制器
        [[NSUserDefaults standardUserDefaults] setObject:curVersion forKey:@"version"];
        
        XMGNewFeatureVc *newVc = [[XMGNewFeatureVc alloc]init];
        self.window.rootViewController = newVc;
    }
    
//    3.显示可见
    [self.window makeKeyAndVisible];
    
    return YES;
}
```

- 注意:这里的版本号名称,百度一查就知道了 

```objc
@"CFBundleShortVersionString"
```