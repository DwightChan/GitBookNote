# NSURLSession实现文件上传
<br/>
##本节知识点:

1. 实现文件上传的步骤
2. 文件上传设置请求体的数据格式
3. 使用NSURLSession上传文件的代码
4. 可以设置代理，在代理方法中监听文件上传进度
5. 如何获得文件的MIMEType类型
6. 关于NSURLSessionConfiguration

--- 
<br/>
##1. 实现文件上传的步骤
- **实现文件上传的步骤**
    - 1.确定请求路径
    - 2.根据URL创建一个可变的请求对象
    - 3.设置请求对象，修改请求方式为POST
    - 4.设置请求头，告诉服务器我们将要上传文件Content-Type.
    - 5.拼接要上传的数据体在请求体中按照既定的格式拼接要上传的文件参数和非文件参数等数据.(见第二个知识点:文件上传设置请求体的数据格式)
        - 拼接文件参数
        - 拼接非文件参数
        - 添加结尾标记
    - 6.创建会话, 发送请求上传文件, 
    - 7.解析服务器返回的数据


- **实现文件上传的代码**

  ```objc
  #import "ViewController.h"

  //分隔字符 : 这个可以随意写, 但一定要保证分隔符保持一致, 
  // 即是指分隔符只能有一种, 不能有多种符号表示分隔符,一般都是定义宏
  //#define Kboundary @"----WebKitFormBoundaryhnASUF5TDdmAE33n"
  #define Kboundary @"sbsbsbsbsbsbsbsbsbsbbsbsbsbsbsbsb"
  #define KnewLine   [[NSString stringWithFormat:@"\r\n"] dataUsingEncoding:NSUTF8StringEncoding]

  @interface ViewController ()
  @end

  @implementation ViewController

  - (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{
      [self updload];
  }
  ```
  ```objc
  - (void)updload{
      // 1. 确定请求路径
      NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/upload"];
      // 2. 创建可以变的请求对象
      NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];
      // 3. 修改请求方式为 post
      request.HTTPMethod = @"POST";
      // 4. 设置请求头部信息, 上传请求
      NSString *header =  [NSString stringWithFormat:@"multipart/form-data; boundary=%@",Kboundary];
      [request setValue:header forHTTPHeaderField:@"Content-Type"];

      // 5. 创建会话
      NSURLSession *session = [NSURLSession sharedSession];

      // 6. 拼接上传的数据 (抽取拼接数据作为一个方法)
      NSData *data = [self getBodyData];
      // 7. 创建上传请求任务, 并执行任务
      /*
       第一个参数:请求对象
       第二个参数:要上传的参数(就是之前需要设置在请求体内部的数据)
       第三个参数:completionHandler 当请求完成的时候回调
       */
      [[session uploadTaskWithRequest:request fromData:data completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {

          // 8. 解析数据
          NSLog(@"%@",[[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

          // 注意: 一定要执行任务
      }] resume];
  }
  ```

--- 
<br/>
##2. 文件上传设置请求体的数据格式
- **注意: 步骤要一模一样, 并且格式中必要的字符(包括空行)一个都不能少 **

  ```objc
  //请求体拼接格式
  //分隔符：----WebKitFormBoundaryhBDKBUWBHnAgvz9c
  //      分隔符可以任意写, 但不可出现中文, 只要是分隔符的地方都要保持一致即可

  //01.文件参数拼接格式

   --分隔符
   Content-Disposition:参数
   Content-Type:参数
   空行
   文件参数

  //02.非文件拼接参数
   --分隔符
   Content-Disposition:参数
   空行
   非文件的二进制数据

  //03.结尾标识
  --分隔符--
  ```
  ```objc
  // 拼接上传的数据
  - (NSData *)getBodyData {
      NSMutableData *data = [NSMutableData data];

      //按照格式来拼接数据
      //1.文件参数
      /*
       --分隔符
       Content-Disposition: form-data; name="file"; filename="Snip20160510_2.png"
       Content-Type: image/png
       空行
       文件数据
       */
      [data appendData:[[NSString stringWithFormat:@"--%@",Kboundary] dataUsingEncoding:NSUTF8StringEncoding]];
      [data appendData:KnewLine];
      //filename = 123.png 表示该文件上传到服务器以什么名称保存
      [data appendData:[@"Content-Disposition: form-data; name=\"file\"; filename=\"Snip20160510_2.png\"" dataUsingEncoding:NSUTF8StringEncoding]];
      [data appendData:KnewLine];

      //Content-Type :文件的数据类型(MIMETYPE)  万能的 MINETYPE: application/octet-stream
      [data appendData:[@"Content-Type: image/png" dataUsingEncoding:NSUTF8StringEncoding]];
      [data appendData:KnewLine];
      [data appendData:KnewLine];

      UIImage *image = [UIImage imageNamed:@"Snip20160510_2"];
      NSData *imageData = UIImagePNGRepresentation(image);
      [data appendData:imageData];
      [data appendData:KnewLine];

      //2.非文件参数
      /*
       --分隔符
       Content-Disposition: form-data; name="username"
       空行
       非文件参数-123
       */
      [data appendData:[[NSString stringWithFormat:@"--%@",Kboundary] dataUsingEncoding:NSUTF8StringEncoding]];
      [data appendData:KnewLine];
      [data appendData:[[NSString stringWithFormat:@"Content-Disposition: form-data; name=\"username\""] dataUsingEncoding:NSUTF8StringEncoding]];
      [data appendData:KnewLine];
      [data appendData:KnewLine];

      [data appendData:[@"cdh" dataUsingEncoding:NSUTF8StringEncoding]];
      [data appendData:KnewLine];

      // 3.结尾标识
      /*--分隔符--*/
      [data appendData:[[NSString stringWithFormat:@"--%@--",Kboundary] dataUsingEncoding:NSUTF8StringEncoding]];

      return  data;
  }
  ```
  
--- 
<br/>

##3. 使用NSURLSession上传文件的代码

- **1. 确定请求路径**
- **2. 创建可以变的请求对象**
- **3. 修改请求方式为 post**
- **4. 设置请求头部信息, 上传请求**
- **5. 创建会话**
- **6. 拼接上传的数据 (抽取拼接数据作为一个方法)**
- **7. 创建上传请求任务, 并执行任务**
- **8. 解析数据(回调)**

  ```objc
  - (void)updload{
      // 1. 确定请求路径
      NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/upload"];
      // 2. 创建可以变的请求对象
      NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];
      // 3. 修改请求方式为 post
      request.HTTPMethod = @"POST";
      // 4. 设置请求头部信息, 上传请求
      NSString *header =  [NSString stringWithFormat:@"multipart/form-data; boundary=%@",Kboundary];
      [request setValue:header forHTTPHeaderField:@"Content-Type"];

      // 5. 创建会话
  //    NSURLSession *session = [NSURLSession sharedSession];

      // 6. 拼接上传的数据 (抽取拼接数据作为一个方法)
      NSData *data = [self getBodyData];
      // 7. 创建上传请求任务, 并执行任务
      /*
       第一个参数:请求对象
       第二个参数:要上传的参数(就是之前需要设置在请求体内部的数据)
       第三个参数:completionHandler 当请求完成的时候回调
               NSData:响应体
               NSURLResponse：响应头
               NSError：请求的错误信息
       */
      [[self.session uploadTaskWithRequest:request fromData:data completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {

          // 8. 解析数据
          NSLog(@"%@",[[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

          // 注意: 一定要执行任务
      }] resume];
  }
  ```

--- 
<br/>
##4. 可以设置代理，在代理方法中监听文件上传进度

- **设置属性, 通过懒加载创建会话任务**
    - 设置代理, 遵循协议, 实现代理方法

  ```objc
  @property (strong, nonatomic) NSURLSession *session;
  ```
  ```objc
  - (NSURLSession *)session{
      if (!_session) {
          // 在这里给单例做配置是统一设置了, 后面所有用到这个单例都是这个配置
          // 设置配置信息
          NSURLSessionConfiguration *config = [NSURLSessionConfiguration defaultSessionConfiguration];

          // 设置请求超时的时间
          config.timeoutIntervalForRequest = 15.0 ;
          //设置是否允许蜂窝网络访问(蜂窝访问是指, 用户的网络是WiFi情况, 2g/3g/4g网络情况)
          config.allowsCellularAccess = YES;
          // 创建会话, 并配置会话, 设置代理
          _session = [NSURLSession sessionWithConfiguration:config delegate:self delegateQueue:[NSOperationQueue mainQueue]];
      }
      return _session;
  }
  ```
  ```objc
  - (void)updload{
      // 1. 确定请求路径
      NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/upload"];
      // 2. 创建可以变的请求对象
      NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];
      // 3. 修改请求方式为 post
      request.HTTPMethod = @"POST";
      // 4. 设置请求头部信息, 上传请求
      NSString *header =  [NSString stringWithFormat:@"multipart/form-data; boundary=%@",Kboundary];
      [request setValue:header forHTTPHeaderField:@"Content-Type"];

      // 5. 创建会话 (直接通过懒加载了)
  //    NSURLSession *session = [NSURLSession sharedSession];

      // 6. 拼接上传的数据 (抽取拼接数据作为一个方法)
      NSData *data = [self getBodyData];
      // 7. 创建上传请求任务, 并执行任务
      /*
       第一个参数:请求对象
       第二个参数:要上传的参数(就是之前需要设置在请求体内部的数据)
       第三个参数:completionHandler 当请求完成的时候回调
       */
      [[self.session uploadTaskWithRequest:request fromData:data completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {    

          // 8. 解析数据
          NSLog(@"%@",[[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

          // 注意: 一定要执行任务
      }] resume];

  }
  ```
  ```objc
  #pragma mark - NSURLSessionDataDelegate
  /*
   调用该方法上传文件数据
   如果文件数据很大，那么该方法会被调用多次
   参数说明：
       bytesSent :本次发送给服务器的数据
       totalBytesSent:已经发送的数据总大小
       totalBytesExpectedToSend:文件的总大小
   */
  - (void)URLSession:(NSURLSession *)session task:(NSURLSessionTask *)task didSendBodyData:(int64_t)bytesSent totalBytesSent:(int64_t)totalBytesSent totalBytesExpectedToSend:(int64_t)totalBytesExpectedToSend{

      NSLog(@"%.2f",1.0 * totalBytesSent / totalBytesExpectedToSend);
  }
  ```


--- 
<br/>
##5. 如何获得文件的MIMEType类型
- **1.直接对该对象发送一个异步网络请求，在响应头中通过response.MIMEType拿到文件的MIMEType类型**

  ```objc
  //如果想要及时拿到该数据，那么可以发送一个同步请求
  - (NSString *)getMIMEType{
      NSString *filePath = @"/Users/chendehao/Desktop/备课/其它/swift.md";

      NSURLResponse *response = nil;
      // 注意: 这里发送的是同步函数, 只有等到了服务区的响应才能确定你文件 MIMEType
      // 会出现程序卡顿现象, 当然如果在子线程中执行就没问题
      [NSURLConnection sendSynchronousRequest:[NSURLRequest requestWithURL:[NSURL fileURLWithPath:filePath]] returningResponse:&response error:nil];
      return response.MIMEType;
  }
  ```
  ```objc
  //对该文件发送一个异步请求，拿到文件的MIMEType
  - (void)MIMEType{

      //    NSString *file = @"file:///Users/chendehao/Desktop/test.png";
      [NSURLConnection sendAsynchronousRequest:[NSURLRequest requestWithURL:[NSURL fileURLWithPath:@"/Users/chendehao/Desktop/test.png"]] queue:[NSOperationQueue mainQueue] completionHandler:^(NSURLResponse * __nullable response, NSData * __nullable data, NSError * __nullable connectionError) {
          //       response.MIMEType
          NSLog(@"%@",response.MIMEType);
      }];
  }
  ```
  
- **2.通过UTTypeCopyPreferredTagWithClass方法**
    - 注意：需要依赖于框架MobileCoreServices

  ```objc
  - (NSString *)mimeTypeForFileAtPath:(NSString *)path
  {
      if (![[[NSFileManager alloc] init] fileExistsAtPath:path]) {
          return nil;
      }

      CFStringRef UTI = UTTypeCreatePreferredIdentifierForTag(kUTTagClassFilenameExtension, (__bridge CFStringRef)[path pathExtension], NULL);
      CFStringRef MIMEType = UTTypeCopyPreferredTagWithClass (UTI, kUTTagClassMIMEType);
      CFRelease(UTI);
      if (!MIMEType) {
          return @"application/octet-stream";
      }
      return (__bridge NSString *)(MIMEType);
  }
  ```

- **代码实现**

  ```objc
  /*
   1)对着该文件发请求,可以得到响应头信息(MIMEtype)
   2)调用C语言的API
   3)百度
   4)通用的二进制数据类型  任意的二进制数据 application/octet-stream
   */

  - (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{
      /*
       1)对着该文件发请求,可以得到响应头信息(MIMEtype)
       2)调用C语言的API
       3)百度
       4)通用的二进制数据类型  任意的二进制数据 application/octet-stream (万能的 MIMEtype)
       */    
      [self getMIMEType];
  }
  ```
  ```objc
  //ppt  --> application/vnd.openxmlformats-officedocument.presentationml.presentation
  // 注意: MIMET 是个专业术语, 全部大写
  - (void)getMIMEType{
      //MIMEType HTTP协议规定的 (大类型/小类型)
      //png  --> image/png
      NSURL *url = [NSURL fileURLWithPath:@"/Users/chendehao/Desktop/Snip20160510_2.png"];
      [[[NSURLSession sharedSession] dataTaskWithURL:url completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {

          // 通过响应头信息得到文件的类型
          NSLog(@"%@",response.MIMEType);
      }] resume];
  }
  ```


--- 
<br/>
##6. 关于NSURLSessionConfiguration

- **作用：可以统一配置NSURLSession,如请求超时等**
- **创建的方式和使用**

  ```objc
  //创建配置的三种方式
  + (NSURLSessionConfiguration *)defaultSessionConfiguration;
  + (NSURLSessionConfiguration *)ephemeralSessionConfiguration;
  + (NSURLSessionConfiguration *)backgroundSessionConfigurationWithIdentifier:(NSString *)identifier NS_AVAILABLE(10_10, 8_0);

  //统一配置NSURLSession
  -(NSURLSession *)session
  {
      if (_session == nil) {

          //创建NSURLSessionConfiguration
          NSURLSessionConfiguration *config = [NSURLSessionConfiguration defaultSessionConfiguration];

          //设置请求超时为10秒钟
          config.timeoutIntervalForRequest = 10;

          //在蜂窝网络情况下是否继续请求上传或下载.
          config.allowsCellularAccess = NO;

          _session = [NSURLSession sessionWithConfiguration:config delegate:self delegateQueue:[NSOperationQueue mainQueue]];
      }
      return _session;
  }
  ```

--- 
<br/>
