# 监测网络状态(Monitoring Network Status)

- **监听网络状态两种方法**:
    - **可以使用AFN框架中的AFNetworkReachabilityManager来监听网络状态的改变**
        - 可以持续实时监测网络状态
    - **可以利用苹果提供的Reachability来监听**。
        - 如果要持续监听,则需要和通知一起使用
        - 程序第一次启动不会监测网络状态,只有网络状态改变的时候后才会有通知


- **建议在开发中直接使用AFN框架处理**。

- **代码示例**

```objc
/*
说明：可以使用AFN框架中的AFNetworkReachabilityManager来监听网络状态的改变，也可以利用苹果提供的Reachability来监听。建议在开发中直接使用AFN框架处理。
 */
//使用AFN框架来检测网络状态的改变
-(void)AFNReachability{
    //1.创建网络监听管理者
    AFNetworkReachabilityManager *manager = [AFNetworkReachabilityManager sharedManager];

    //2.监听网络状态的改变
    /*
     AFNetworkReachabilityStatusUnknown          = 未知
     AFNetworkReachabilityStatusNotReachable     = 没有网络
     AFNetworkReachabilityStatusReachableViaWWAN = 3G
     AFNetworkReachabilityStatusReachableViaWiFi = WIFI
     */
    [manager setReachabilityStatusChangeBlock:^(AFNetworkReachabilityStatus status) {
        switch (status) {
            case AFNetworkReachabilityStatusUnknown:
                NSLog(@"未知");
                break;
            case AFNetworkReachabilityStatusNotReachable:
                NSLog(@"没有网络");
                break;
            case AFNetworkReachabilityStatusReachableViaWWAN:
                NSLog(@"3G");
                break;
            case AFNetworkReachabilityStatusReachableViaWiFi:
                NSLog(@"WIFI");
                break;

            default:
                break;
        }
    }];

    //3.开始监听
    [manager startMonitoring];
}
```
```objc
//使用苹果提供的Reachability来检测网络状态，如果要持续监听网络状态的概念，需要结合通知一起使用。
//提供下载地址：https://developer.apple.com/library/ios/samplecode/Reachability/Reachability.zip

-(void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{
    //1.注册一个通知
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(networkChange) name:kReachabilityChangedNotification object:nil];

    //2.拿到一个对象，然后调用开始监听方法
    Reachability *r = [Reachability reachabilityForInternetConnection];
    [r startNotifier];

    //持有该对象，不要让该对象释放掉
    self.r = r;
}

//当控制器释放的时候，移除通知的监听
-(void)dealloc{
    [[NSNotificationCenter defaultCenter] removeObserver:self];
}

-(void)networkChange
{
    //获取当前网络的状态
   if ([Reachability reachabilityForInternetConnection].currentReachabilityStatus == ReachableViaWWAN){
        NSLog(@"当前网络状态为3G");
        return;
    }
    if ([Reachability reachabilityForLocalWiFi].currentReachabilityStatus == ReachableViaWiFi){
        NSLog(@"当前网络状态为wifi");
        return;
    }
    NSLog(@"当前没有网络");
}
```

---
<br/>