[toc]

----



# iOS 唤起APP之Universal Link(通用链接)

> `iOS 9`之前，一直使用的是`URL Schemes`技术来从外部对`App`进行跳转，但是`iOS`系统中进行`URL Schemes`跳转的时候如果没有安装`App`，会提示`Cannot open Page`的提示，而且当注册有多个`scheme`相同的时候，目前没有办法区分，但是从`iOS 9`起可以使用`Universal Links`技术进行跳转页面，这是一种体验更加完美的解决方案

- 什么是`Universal Link`（通用链接） `Universal Link`是`Apple`在`iOS 9`推出的一种能够方便的通过传统`HTTPS`链接来启动`APP`的功能。如果你的应用支持`Universal Link`，当用户点击一个链接时可以跳转到你的网站并获得无缝重定向到对应的`APP`，且不需要通过`Safari`浏览器。如果你的应用不支持的话，则会在`Safari`中打开该链接
- 支持`Universal Link`（通用链接） 先决条件：必须有一个支持`HTTPS`的域名，并且拥有该域名下上传到根目录的权限（为了上传`Apple`指定文件）
- **集成步骤**

1. 开发者中心配置 找到对应的`App ID`，在`Application Services`列表里有`Associated Domains`一条，把它变为`Enabled`就可以了

   ![配置App ID支持Associated Domains](https://user-gold-cdn.xitu.io/2019/11/6/16e3fd1de61b6fe2?imageView2/0/w/1280/h/960/ignore-error/1)

   

2. 工程配置 `targets->Capabilites->Associated Domains`，在其中的`Domains`中填入你想支持的域名，必须以`applinks:`为前缀，如：`applinks:domain`

   ![配置项目中的Associated Domains](https://user-gold-cdn.xitu.io/2019/11/6/16e3fd1de624bad5?imageView2/0/w/1280/h/960/ignore-error/1)

   

3. 配置指定文件 创建一个内容为`json`格式的文件，苹果将会在合适的时候，从我们在项目中填入的域名请求这个文件。这个文件名必须为`apple-app-site-association`，切记没有`后缀名`，文件内容大概是这样子：

```
{
    "applinks": {
        "apps": [],
        "details": [
            {
                "appID": "9JA89QQLNQ.com.apple.wwdc",
                "paths": [ "/wwdc/news/", "/videos/wwdc/2015/*"]
            },
            {
                "appID": "ABCD1234.com.apple.wwdc",
                "paths": [ "*" ]
            }
        ]
    }
}
复制代码
```

`appID`：组成方式是`TeamID.BundleID`。如上面的`9JA89QQLNQ`就是`teamId`。登陆开发者中心，在`Account -> Membership`里面可以找到`Team ID` `paths`：设定你的`app`支持的路径列表，只有这些指定路径的链接，才能被`app`所处理。`*`的写法代表了可识别域名下所有链接

1. 上传该文件 上传该文件到你的域名所对应的`根目录`或者`.well-known目录`下，这是为了苹果能获取到你上传的文件。上传完后，先访问一下，看看是否能够获取到，当你在浏览器中输入这个文件链接后，应该是直接下载`apple-app-site-association`文件
2. 代码中的相关支持 当点击某个链接，可以直接进我们的`app`，但是我们的目的是要能够获取到用户进来的链接，根据链接来展示给用户相应的内容，我们需要在工程里实现`AppDelegate`对应的方法：

```
- (BOOL)application:(UIApplication *)application continueUserActivity:(NSUserActivity *)userActivity restorationHandler:(void (^)(NSArray * _Nullable))restorationHandler {
    // NSUserActivityTypeBrowsingWeb 由Universal Links唤醒的APP
    if ([userActivity.activityType isEqualToString:NSUserActivityTypeBrowsingWeb]){
        NSURL *webpageURL = userActivity.webpageURL;
        NSString *host = webpageURL.host;
        if ([host isEqualToString:@"api.r2games.com.cn"]){
            //进行我们的处理
            NSLog(@"TODO....");
        }else{
            NSLog(@"openurl");
            [[UIApplication sharedApplication] openURL:webpageURL options:nil completionHandler:nil];
            // [[UIApplication sharedApplication] openURL:webpageURL];
        }
    }
    return YES;
}
复制代码
```

苹果为了方便开发者，提供了一个[网页验证](https://search.developer.apple.com/appsearch-validation-tool/)我们编写的这个`apple-app-site-association`是否合法有效

- **Universal Link（通用链接）注意点**

1. `Universal Link`跨域 `Universal Link`有跨域问题，`Universal Link`必须要求跨域，如果不跨域，就不会跳转（`iOS 9.2`之后的改动） 假如当前网页的域名是`A`，当前网页发起跳转的域名是`B`，必须要求`B`和`A`是不同域名才会触发`Universal Link`，如果`B`和`A`是相同域名，只会继续在当前`WebView`里面进行跳转，哪怕你的`Universal Link`一切正常，根本不会打开`App`
2. `Universal Link`请求`apple-app-site-association`时机

- 当我们的`App`在设备上第一次运行时，如果支持`Associated Domains`功能，那么`iOS`会自动去`GET`定义的`Domain`下的`apple-app-site-association`文件
- `iOS`会先请求`https://domain.com/.well-known/apple-app-site-association`，如果此文件请求不到，再去请求`https://domain.com/apple-app-site-association`，所以如果想要避免服务器接收过多`GET`请求，可以直接把`apple-app-site-association`放在`./well-known`目录下
- 服务器上`apple-app-site-association`的更新不会让`iOS`本地的`apple-app-site-association`同步更新，即`iOS`只会在`App`第一次启动时请求一次，以后除非`App`更新或重新安装，否则不会在每次打开时请求`apple-app-site-association`
- **Universal Link的好处**

1. 之前的`Custom URL scheme`是自定义的协议，因此在没有安装该`app`的情况下是无法直接打开的。而`Universal Links`本身就是一个能够指向`web`页面或者`app`内容页的标准`web link`，因此能够很好的兼容其他情况
2. `Universal links`是从服务器上查询是哪个`app`需要被打开，因此不存在`Custom URL scheme`那样名字被抢占、冲突的情况
3. `Universal links`支持从其他`app`中的`UIWebView`中跳转到目标`app`
4. 提供`Universal link`给别的`app`进行`app`间的交流时，对方并不能够用这个方法去检测你的`app`是否被安装（之前的`custom scheme URL`的`canOpenURL`方法可以）

-----

> 转载 https://juejin.im/post/5dc28383518825108876bd74
>
> [附：原作者的博客地址](https://gsl201600.github.io/2019/11/06/iOS唤起APP之Universal Link/)
>
> 