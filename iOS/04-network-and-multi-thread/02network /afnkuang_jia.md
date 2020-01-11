# AFN框架

<br/>

##本节知识点:
1. AFN内部结构
2. AFN的基本使用
    1. 发送 get 请求
    2. 发送 post 请求
    3. 文件下载
    4. 文件上传
3. 使用AFN进行序列化处理
4. AFN使用技巧
5. 监测网络状态
    1. AFN框架监测网络状态
    2. 苹果(apple)提供的Reachability来检测网络状态
6. HTTPS的基本使用


---
<br/>
##1. AFN内部结构



- **NSURLConnection**
    + AFURLConnectionOperation(已经被废弃)
    + AFHTTPRequestOperation(已经被废弃)
    + AFHTTPRequestOperationManager(封装了常用的 HTTP 方法)(已经被废弃)
        * 属性
            * baseURL :AFN建议开发者针对 AFHTTPRequestOperationManager 自定义个一个单例子类，设置 baseURL, 所有的网络访问，都只使用相对路径即可
            * requestSerializer :请求数据格式/默认是二进制的 HTTP
            * responseSerializer :响应的数据格式/默认是 JSON 格式
            * operationQueue
            * reachabilityManager :网络连接管理器
        * 方法
            * manager :方便创建管理器的类方法
            * HTTPRequestOperationWithRequest :在访问服务器时，如果要告诉服务器一些附加信息，都需要在 Request 中设置
            * GET
            * POST


- **NSURLSession**
    + AFURLSessionManager
    + AFHTTPSessionManager(封装了常用的 HTTP 方法)
        * GET
        * POST
        * UIKit + AFNetworking 分类
        * NSProgress :利用KVO


- **半自动的序列化&反序列化的功能**
    + AFURLRequestSerialization :请求的数据格式/默认是二进制的
    + AFURLResponseSerialization :响应的数据格式/默认是JSON格式


- **附加功能**
    + 安全策略
        * HTTPS
        * AFSecurityPolicy
    + 网络检测
        * 对苹果的网络连接检测做了一个封装
        * AFNetworkReachabilityManager


- **建议:** 可以学习下AFN对 UIKit 做了一些分类, 对自己能力提升是非常有帮助的


--- 
<br/>

##2. AFN的基本使用

- **发送 GET 请求**

  ```objc
  - (void)get{
      // 1. 创建一个会话管理者
      AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];

      // 封装参数
      NSDictionary *dict = @{
                             @"username": @"520it",
                             @"pwd":@"520it",
                             @"type":@"JSON"
                             };
      //3.发送GET请求 // 如果是 POST 请求则只要将 GET 改写成 POST 即可,
      //  虽然将参数提取了, 但内部实现还是之前的 get 请求和 post 请求的路径,
      //  只不过是封装的比较好
      /*
       以前 http://120.25.226.186:32812/login?username=123&pwd=123&type=JSON
       AFN http://120.25.226.186:32812/login
       第一个参数:请求路径(NSString)+
               注意:
                   1. 不管是get请求还是 post 请求, 都不需要加参数
                   2. 这里传的是 NSString 类型, 而不是 NSURL 类型
       第二个参数:发送给服务器的参数数据
       第三个参数:progress 进度回调
       第四个参数:success  成功之后的回调(此处的成功或者是失败指的是整个请求)
               task:请求任务
               responseObject:注意!!!响应体信息--->(内部已经完成 json--->oc))
                               有别于前面的 response 是响应头信息
               task.response: 响应头信息
       第五个参数:failure 失败之后的回调
       */
      [manager GET:@"http://120.25.226.186:32812/login"  parameters:dict progress:nil success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
          NSLog(@"success--%@--%@",[responseObject class],responseObject );
      } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
          NSLog(@"failure-- %@",error);
      }];
  }
  ```

- **发送 POST 请求**

  ```objc
  - (void)post{
      // 1. 创建一个会话管理者
      AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];

      // 封装参数
      NSDictionary *dict = @{
                             @"username": @"520it",
                             @"pwd":@"520it",
                             @"type":@"JSON"
                             };
      //3.发送GET请求 // 如果是 POST 请求则只要将 GET 改写成 POST 即可,
      //  虽然将参数提取了, 但内部实现还是之前的 get 请求和 post 请求的路径,
      //  只不过是封装的比较好
      [manager POST:@"http://120.25.226.186:32812/login"  parameters:dict progress:nil success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
          NSLog(@"success--%@--%@",[responseObject class],responseObject );
      } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
          NSLog(@"failure-- %@",error);
      }];
  }
  ```

- **使用AFN下载文件**

  ```objc
  - (void)download{
      // 1.创建会话管理了者
      AFHTTPSessionManager *manger= [AFHTTPSessionManager manager];

      // 2.确定请求路径
      NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/resources/videos/minion_02.mp4"];

      // 3. 创建请求对象
      NSURLRequest *request = [NSURLRequest requestWithURL:url];

      // 4. 发送网络请求下载文件
      /*
       第一个参数:请求对象
       第二个参数:progress 进度回调
       downloadProgress
       @property int64_t totalUnitCount;
       @property int64_t completedUnitCount;
       第三个参数:destination 让我们告诉系统应该把文件存放到什么地方, 内部自动的完成剪切处理
       注意: 是通过这里个返回值告诉系统
       第四个参数: completionHandler 完成之后的回调
       response 响应头信息
       filePath  文件最终的存储路径
       error 错误信息
       */
      [[manger downloadTaskWithRequest:request progress:^(NSProgress * _Nonnull downloadProgress) {
          NSLog(@"%f",1.0 * downloadProgress.completedUnitCount / downloadProgress.totalUnitCount);
      } destination:^NSURL * _Nonnull(NSURL * _Nonnull targetPath, NSURLResponse * _Nonnull response) {
          // 拼接文件全路径
          NSString *fullpath = [[NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES)lastObject] stringByAppendingPathComponent:response.suggestedFilename];

          return [NSURL fileURLWithPath:fullpath];
      } completionHandler:^(NSURLResponse * _Nonnull response, NSURL * _Nullable filePath, NSError * _Nullable error) {

          NSLog(@"%@",filePath);
          //注意: 一定要开启任务
      }] resume];
  }
  ```

- **AFN文件上传有 4 种方式:**

    - 1.文件上传拼接数据的第一种方式

  ```objc
  [formData appendPartWithFileData:data name:@"file" fileName:@"xxoo.png" mimeType:@"application/octet-stream"];
  ```

    - 2.文件上传拼接数据的第二种方式(第一种的简写)

  ```objc
  [formData appendPartWithFormData:data name:@"file"];
  ```
    - 3.文件上传拼接数据的第三种方式

  ```objc
   [formData appendPartWithFileURL:fileUrl name:@"file" fileName:@"xx.png" mimeType:@"application/octet-stream" error:nil];
   ```

    - 4.文件上传拼接数据的第四种方式(第三中的简写)

  ```objc
   [formData appendPartWithFileURL:fileUrl name:@"file" error:nil];
  ```

  - 5.【注】在资料中已经提供了一个用于文件上传的分类。


- **示例代码**

  ```objc
  - (void)upload{
      // 1. 创建会话管理者
      AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];
      // 2. 发送请求上传文件
      /*
       // 这个方法要一点一点的拼接上传数据, 不方便, 用另一中快捷方法
       [manager uploadTaskWithRequest:<#(nonnull NSURLRequest *)#> fromData:<#(nullable NSData *)#> progress:<#^(NSProgress * _Nonnull uploadProgress)uploadProgressBlock#> completionHandler:<#^(NSURLResponse * _Nonnull response, id  _Nullable responseObject, NSError * _Nullable error)completionHandler#>]
       */
      /*
       第一个参数:请求路径(NSString)
       第二个参数:非文件参数, (本例子中服务器写的这个地方可以不用上传数据, 所以就用 nil )
       第三个参数:constructingBodyWithBlock 拼接数据(告诉AFN要上传的数据是哪些)
       第四个参数:progress 进度回调
       第五个参数:success 成功回调
       responseObject:响应体
       第六个参数:failure 失败的回调
       */
      [manager POST:@"http://120.25.226.186:32812/upload" parameters:nil constructingBodyWithBlock:^(id<AFMultipartFormData>  _Nonnull formData) {

  //        方法一:
  //        使用 NSData 类型通信上传数据
  //        NSData *data = [NSData dataWithContentsOfFile:@"/Users/chendehao/Desktop/Snip20160510_2.png"];
  //              第一种
  //        [formData appendPartWithFileData:data name:@"file" fileName:@"12.png" mimeType:@"image/png"];
  //              第二种 (第一种的简写)
  //        [formData appendPartWithFormData:data name:@"file"];
  //        方法二:
  //        使用 NSURL 类型通信上传数据
          NSURL *url = [NSURL fileURLWithPath:@"/Users/chendehao/Desktop/Snip20160510_2.png"];
  //              第三种
  //        [formData appendPartWithFileURL:url name:@"file" fileName:@"123.png" mimeType:@"application/octet-stream" error:nil];
  //              第四种(第三种的简写)
          [formData appendPartWithFileURL:url name:@"file" error:nil];
      } progress:^(NSProgress * _Nonnull uploadProgress) {
          // 计算上传进度
          NSLog(@"%f", 1.0 * uploadProgress.completedUnitCount /  uploadProgress.totalUnitCount);

      } success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
          NSLog(@"success--%@",responseObject);
      } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
          NSLog(@"failure -- %@",error);
      }];
  }
  ```


--- 
<br/>
##3. 使用AFN进行序列化处理

- **1.AFN它内部默认把服务器响应的数据当做json来进行解析，所以如果服务器返回给我的不是JSON数据那么请求报错，这个时候需要设置AFN对响应信息的解析方式。AFN提供了三种解析响应信息的方式，分别是：**
    - AFXMLParserResponseSerializer----XML
    - AFHTTPResponseSerializer----------默认二进制响应数据
    - AFJSONResponseSerializer----------JSON


- **2.还有一种情况就是服务器返回给我们的数据格式不太一致（开发者工具Content-Type:text/xml）,那么这种情况也有可能请求不成功。解决方法:**
    - 直接在源代码中修改，添加相应的Content-Type
    - 拿到这个属性，添加到它的集合中


- **相关代码**

  ```objc
  -(void)srializer
  {
      //1.创建请求管理者，内部基于NSURLSession
      AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];

      /* 知识点1：设置AFN采用什么样的方式来解析服务器返回的数据*/

      //如果返回的是XML，那么告诉AFN，响应的时候使用XML的方式解析 
      // 注意: 解析 xml 格式时, 要创建解析器, 给解析通过解析对象的代理方法来解析数据, 
      manager.responseSerializer = [AFXMLParserResponseSerializer serializer];

      //如果返回的就是二进制数据，那么采用默认二进制的方式来解析数据
      //manager.responseSerializer = [AFHTTPResponseSerializer serializer];

      //采用JSON的方式来解析数据 , 默认是 JSON 方式 ,因此可以不写
      //manager.responseSerializer = [AFJSONResponseSerializer serializer];

      /*知识点2 告诉AFN，再序列化服务器返回的数据的时候，支持此种类型*/
      [AFJSONResponseSerializer serializer].acceptableContentTypes = [NSSet setWithObject:@"text/xml"];

      //2.把所有的请求参数通过字典的方式来装载，GET方法内部会自动把所有的键值对取出以&符号拼接并最后用？符号连接在请求路径后面
      NSDictionary *dict = @{
                             @"username":@"223",
                             @"pwd":@"ewr",
                             @"type":@"XML"
                             };

      //3.发送GET请求
      [manager GET:@"http://120.25.226.186:32812/login" parameters:dict success:^(NSURLSessionDataTask * _Nonnull task, id  _Nonnull responseObject) {

          //4.请求成功的回调block
          NSLog(@"%@",[responseObject class]);
      } failure:^(NSURLSessionDataTask * _Nonnull task, NSError * _Nonnull error) {

          //5.请求失败的回调，可以打印error的值查看错误信息
          NSLog(@"%@",error);
      }];
  }
  ```
  ```objc
  #pragma  mark - Methods
  - (void)json{

      // 1. 创建一个会话管理者
      AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];

      /*
       1)afn内部默认已经完成了JSON解析工作
       优点:方便
       缺点:如果服务器返回的数据不是JSON会报错
       */
       NSDictionary *dict = @{@"type":@"JSON"};
      // 2. 发送请求
      [manager GET:@"http://120.25.226.186:32812/video" parameters:dict progress:nil success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
          NSLog(@"%@---%@",[responseObject class],responseObject);
      } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
          NSLog(@"%@----",error);
      }];
  }
  ```
  ```objc
  -(void)xml{
      // 1. 创建一个会话管理者
      AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];
      // afn内部默认已经完成了JSON解析工作 所以我们必须修改为 xml 来解析数据
      // 注意: 这里一定要设置为 xml 的方式来解析数据
      manager.responseSerializer = [AFXMLParserResponseSerializer serializer];
      NSDictionary *dict = @{@"type":@"XML"};
      // 2. 发送请求
      [manager GET:@"http://120.25.226.186:32812/video" parameters:dict progress:nil success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {

          // 1. 创建解析器
          NSXMLParser *parser = (NSXMLParser *)responseObject;

          // 2. 设置代理
          parser.delegate = self;

          // 3. 开始解析
          [parser parse];

          NSLog(@"%@---%@",[responseObject class],responseObject);
      } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
          NSLog(@"%@----",error);
      }];
  }

  #pragma mark - NSXMLParserDelegate
  - (void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName attributes:(NSDictionary<NSString *,NSString *> *)attributeDict{
      // 这里只是简单将每个元素打印出来, 没有添加到数组中
      NSLog(@"%@----%@", elementName,attributeDict);
  }
  ```
  ```objc
  // 服务器返回的既不是json 也不是 xml , 而是二进制数据的时候就不做处理
  - (void)httpData{
      // 1. 穿件会话管理者
      AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];

      // 设置不做处理
      manager.responseSerializer = [AFHTTPResponseSerializer serializer];

      // 2. 发送请求
      [manager GET:@"http://120.25.226.186:32812/resources/images/minion_02.png" parameters:nil progress:nil success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {

          NSLog(@"%@---%@",[responseObject class],responseObject);
          NSLog(@"%@",task);

      } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
          NSLog(@"%@---------",error);
      }];
  }
  ```

---
<br />

##4. AFN使用技巧


- 1.在开发的时候可以创建一个工具类，继承自我们的AFN中的请求管理者，再控制器中真正发请求的代码使用自己封装的工具类。
- 2.这样做的优点是以后如果修改了底层依赖的框架，那么我们修改这个工具类就可以了，而不用再一个一个的去修改。
- 3.该工具类一般提供一个单例方法，在该方法中会设置一个基本的请求路径。
- 4.该方法通常还会提供对GET或POST请求的封装。
- 5.在外面的时候通过该工具类来发送请求
- 6.单例方法：

  ```objc
  + (instancetype)shareNetworkTools
  {
      static XMGNetworkTools *instance;
      static dispatch_once_t onceToken;
      dispatch_once(&onceToken, ^{
          // 注意: BaseURL中一定要以/结尾
          instance = [[self alloc] initWithBaseURL:[NSURL URLWithString:@"http://120.25.226.186:32812/"]];
      });
      return instance;
  }
  ```

--- 
<br/>

##5. 监测网络状态

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
##6. HTTPS的基本使用

- **1.https简单说明**
    - HTTPS（全称：Hyper Text Transfer Protocol over Secure Socket Layer），是以安全为目标的HTTP通道，简单讲是HTTP的安全版。
    - 即HTTP下加入SSL层，HTTPS的安全基础是SSL，因此加密的详细内容就需要SSL。 它是一个URI scheme（抽象标识符体系），句法类同http:体系。用于安全的HTTP数据传输。
    - https: URL表明它使用了HTTP，但HTTPS存在不同于HTTP的默认端口及一个加密/身份验证层（在HTTP与TCP之间）。


- **2.HTTPS和HTTP的区别主要为以下四点：**
    - 一、https协议需要到ca申请证书，一般免费证书很少，需要交费。
    - 二、http是超文本传输协议，信息是明文传输，https 则是具有安全性的ssl加密传输协议。
    - 三、http和https使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443。
    - 四、http的连接很简单，是无状态的；HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全。


- **3.简单说明**
    - HTTPS的主要思想是在不安全的网络上创建一安全信道，并可在使用适当的加密包和服务器证书可被验证且可被信任时，对窃听和中间人攻击提供合理的保护。
    - HTTPS的信任继承基于预先安装在浏览器中的证书颁发机构（如VeriSign、Microsoft等）（意即“我信任证书颁发机构告诉我应该信任的”）。
    - 因此，一个到某网站的HTTPS连接可被信任，如果服务器搭建自己的https 也就是说采用自认证的方式来建立https信道，这样一般在客户端是不被信任的。
    - 所以我们一般在浏览器访问一些https站点的时候会有一个提示，问你是否继续。


- **4.对开发的影响。**
    - 如果是自己使用NSURLSession来封装网络请求，涉及代码如下。

  ```objc
  - (void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event
  {
      NSURLSession *session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:self delegateQueue:[NSOperationQueue mainQueue]];

      NSURLSessionDataTask *task =  [session dataTaskWithURL:[NSURL URLWithString:@"https://www.apple.com"] completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
          NSLog(@"%@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);
      }];
      [task resume];
  }

  /*
   只要请求的地址是HTTPS的, 就会调用这个代理方法
   我们需要在该方法中告诉系统, 是否信任服务器返回的证书
   Challenge: 挑战 质问 (包含了受保护的区域)
   protectionSpace : 受保护区域
   NSURLAuthenticationMethodServerTrust : 证书的类型是 服务器信任
   */
  - (void)URLSession:(NSURLSession *)session didReceiveChallenge:(NSURLAuthenticationChallenge *)challenge completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition, NSURLCredential *))completionHandler
  {
      //    NSLog(@"didReceiveChallenge %@", challenge.protectionSpace);
      NSLog(@"调用了最外层");
      // 1.判断服务器返回的证书类型, 是否是服务器信任
      if ([challenge.protectionSpace.authenticationMethod isEqualToString:NSURLAuthenticationMethodServerTrust]) {
          NSLog(@"调用了里面这一层是服务器信任的证书");
          /*
           NSURLSessionAuthChallengeUseCredential = 0,                     使用证书
           NSURLSessionAuthChallengePerformDefaultHandling = 1,            忽略证书(默认的处理方式)
           NSURLSessionAuthChallengeCancelAuthenticationChallenge = 2,     忽略书证, 并取消这次请求
           NSURLSessionAuthChallengeRejectProtectionSpace = 3,            拒绝当前这一次, 下一次再询问
           */
  //        NSURLCredential *credential = [NSURLCredential credentialForTrust:challenge.protectionSpace.serverTrust];

          NSURLCredential *card = [[NSURLCredential alloc]initWithTrust:challenge.protectionSpace.serverTrust];
          completionHandler(NSURLSessionAuthChallengeUseCredential , card);
      }
  }
  ```


- **5.ATS**
    - iOS9中新增App Transport Security（简称ATS）特性, 让原来请求时候用到的HTTP，全部都转向TLS1.2协议进行传输。
    - 这意味着所有的HTTP协议都强制使用了HTTPS协议进行传输。
    - 如果我们在iOS9下直接进行HTTP请求是会报错。系统会告诉我们不能直接使用HTTP进行请求，需要在Info.plist中控制ATS的配置。
        - "NSAppTransportSecurity"是ATS配置的根节点，配置了节点表示告诉系统要走自定义的ATS设置。
        - "NSAllowsAritraryLoads"节点控制是否禁用ATS特性，设置YES就是禁用ATS功能。
    - 有两种解决方法，一种是修改配置信息继续使用以前的设置。
        - 另一种解决方法是所有的请求都基于基于"TLS 1.2"版本协议。（该方法需要严格遵守官方的规定，如选用的加密算法、证书等）

    - **使用AFNetworking框架**
        - AFSecurityPolicy，内部有三个重要的属性，如下：
            - AFSSLPinningMode SSLPinningMode; 该属性标明了AFSecurityPolicy是以何种方式来验证
            - BOOL allowInvalidCertificates; 是否允许不信任的证书通过验证，默认为NO
            - BOOL validatesDomainName; 是否验证主机名，默认为YES


- **注意:如果HTTPS服务器满足ATS默认的条件，而且SSL证书是通过权威的CA机构认证过的，那么什么都不用做。如果上面的条件中有任何一个不成立，那么都只能修改ATS配置。**

  ```objc
  /*
   ATS默认的条件
   1)服务器TLS版本至少是1.2版本
   2)连接加密只允许几种先进的加密
   3)证书必须使用SHA256或者更好的哈希算法进行签名，要么是2048位或者更长的RSA密钥，要么就是256位或更长的ECC密钥。
   */
  AFSecurityPolicy，内部有三个重要的属性，如下：

  AFSSLPinningMode SSLPinningMode;    //该属性标明了AFSecurityPolicy是以何种方式来验证
  BOOL allowInvalidCertificates;      //是否允许不信任的证书通过验证，默认为NO
  BOOL validatesDomainName;           //是否验证主机名，默认为YES

  "AFSSLPinningMode"枚举类型有三个值，分别是AFSSLPinningModeNone、AFSSLPinningModePublicKey、AFSSLPinningModeCertificate。

  "AFSSLPinningModeNone"代表了AFSecurityPolicy不做更严格的验证，"只要是系统信任的证书"就可以通过验证，不过，它受到allowInvalidCertificates和validatesDomainName的影响；

  "AFSSLPinningModePublicKey"是通过"比较证书当中公钥(PublicKey)部分"来进行验证，通过SecTrustCopyPublicKey方法获取本地证书和服务器证书，然后进行比较，如果有一个相同，则通过验证，此方式主要适用于自建证书搭建的HTTPS服务器和需要较高安全要求的验证；

  "AFSSLPinningModeCertificate"则是直接将本地的证书设置为信任的根证书，然后来进行判断，并且比较本地证书的内容和服务器证书内容是否相同，来进行二次判断，此方式适用于较高安全要求的验证。

  如果HTTPS服务器满足ATS默认的条件，而且SSL证书是通过权威的CA机构认证过的，那么什么都不用做。如果上面的条件中有任何一个不成立，那么都只能修改ATS配置。
  ```
  ```objc
  - (void)viewDidLoad {
      [super viewDidLoad];

      AFHTTPSessionManager *manager = [AFHTTPSessionManager  manager];

      // 设置请求方式
      // 设置响应
      manager.responseSerializer = [AFHTTPResponseSerializer serializer];
      // 允许接收无效的证书, 默认是 NO
      manager.securityPolicy.allowInvalidCertificates = YES;
      // 不验证域名
      manager.securityPolicy.validatesDomainName = NO;

      // 注意: 这个链接有SSL 证书, 但没有通过权威的 CA认证, 所以除了上面要写上两行代码配置之外, 还要修改 info.plist 文件
      [manager GET:@"https://kyfw.12306.cn/otn" parameters:nil progress:nil success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
          NSLog(@"%@",[[NSString alloc]initWithData:responseObject encoding:NSUTF8StringEncoding]);
          NSLog(@"%@",[[NSString alloc]initWithData:responseObject encoding:NSUTF8StringEncoding]);

      } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
          NSLog(@"%@",error);
          NSLog(@"-------------");
      }];
  }
  ```

---
<br/>