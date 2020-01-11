# NSURLConnection基本使用
<br/>

##0. 本节知识点:
1. NSURLConnection同步请求（GET-SendSync）
2. NSURLConnection异步请求（GET-SendAsync）
3. NSURLConnection异步请求（GET-代理）
4. NSURLConnection发送POST请求
5. URL中文转码问题
6. NSURLConnection和Runloop（面试）

---
<br/>
##1. NSURLConnection同步请求（GET-SendSync）
- **发送网络请求的步骤**
    - **(1) 确定请求路径**
        - 创建一个NSURL对象，设置请求路径
    - **(2) 创建一个请求对象**
        - 传入NSURL创建一个NSURLRequest对象，设置请求头和请求体
    - **(3) 定义一个响应对象, 直接赋值为 nil 用于接收响应的数据**
        - 一般使用 NSURLResponse 的子类 NSHTTPURLResponse 
    - **(4) 使用`[NSURLConnection  sendSynchronousRequest: returningResponse: error:]`方法发送网络请求**
        - 第一个参数: 是请求对象
        - 第二个参数: 是接收响应对象的地址
        - **NSURLConnection同步请求就只有这个方法, 该方法是有返回值的,返回值类型 NSData **
    - **(5)接收到服务器的响应后，解析响应体**



- **发送同步请求是阻塞式的,如果该请求没有完成那么后面的将不会得到执行**


- **相关代码**

  ```objc
  //NSURLConnection同步请求（GET）
  -(void)sendSync
  {
      //1.确定请求路径
      NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/login?username=520it&pwd=520&type=JSON"];

      //2.创建请求对象
      //  该方法内部会提供一个默认的请求头信息, 默认发送的就是GET请求
      NSURLRequest *request =[NSURLRequest requestWithURL:url];

      //3.发送请求
      //3.1 响应头信息
      //NSHTTPURLResponse 继承 NSURLResponse
      //NSHTTPURLResponse
      NSHTTPURLResponse *response = nil; // 响应头部信息

      //请求:请求头&请求体(X)
      //响应:响应头&响应体(data)

      //发送请求的方法:同步方法|异步方法
      /*
       第一个参数:请求对象
       第二个参数:响应头信息; 当该方法执行完毕之后，该参数被赋值(注意: 传的是地址)
       第三个参数:错误信息，如果请求失败，则error有值, 成功是没有值得
       返回值: NSData 类型 响应体信息
       */
      //发送同步请求是阻塞式的,如果该请求没有完成那么后面的将不会得到执行
      NSData *data = [NSURLConnection sendSynchronousRequest:request returningResponse:&response error:nil];
      // NSURLConnection 在9.0 版本之后才被弃用的, 所有如果对于这个方法有警告, 可以修改部署版本信息为9.0 之前的就不会有警告了

      // 打印响应头部信息
      NSLog(@"%@",response);
      // 注意: 这里的 statusCode 的属性是 NSHTTPURLResponse 才有的, 他的父类没有这个属性
      NSLog(@"%zd",response.statusCode);

      //4.解析数据
      /**
       第一个参数: 需要解析的数据
       第二个参数: 编码格式
       */
      NSLog(@"%@",[[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding]);
  }
  ```

---
<br/>
##2. NSURLConnection异步请求（GET-SendAsync）
- **发送网络请求的步骤**
    - **(1) 设置请求路径**
    - **(2) 创建请求对象（默认是GET请求，且已经默认包含了请求头）**
    - **(3) 使用NSURLConnection发送请求**
        - 使用`[NSURLConnection  sendAsynchronousRequest:queue:completionHandler:]`方法发送网络请求
        - NSURLConnection异步请求, 也只有这一个方法
        - **注意**: 第二个参数传输的是队列, 表示的是回调是在哪个线程中回调
    - **(4) 接收到服务器的响应后，解析响应体**


- **该方法不会卡住当前线程，网络请求任务是异步执行的**


- **相关代码**

  ```objc
  // NSURLConnection异步请求（GET-SendAsync）
  -(void)sendAsync
  {
      //1.请求路径
      NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/login?username=520it&pwd=111&type=JSON"];

      //2.创建请求对象
      NSURLRequest *request = [NSURLRequest requestWithURL:url];

      //3.发送异步请求
      /*
       第一个参数：请求对象
       第二个参数：回调方法在哪个线程中执行，如果是主队列则block在主线程中执行，非主队列则在子线程中执行
       第三个参数：completionHandler：接受到响应的时候执行该block中的代码, 只要完成(不管是成功还是失败)就回调
               response：响应头信息
               data：响应体
       connectionError：错误信息，如果请求失败，那么该参数有值
       */
      [NSURLConnection sendAsynchronousRequest:request queue:[NSOperationQueue mainQueue] completionHandler:^(NSURLResponse * _Nullable response, NSData * _Nullable data, NSError * _Nullable connectionError) {

          if(connectionError == nil)
          {
              //4.解析数据
              NSLog(@"%@",[[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding]);
          }
      }];

      NSLog(@"---end--");
  }
  ```

---
<br/>

##3. NSURLConnection异步请求（GET-代理）
- **发送网络请求的步骤**

    - **（1）确定请求路径**
    - **（2）创建请求对象**
    - **（3）创建NSURLConnection对象并设置代理 (三种方法)**
        - 一个类方法创建对象, 设置代理,并自动开启请求`connectionWithRequest:delegate:`
        - 有两个 alloc / initWithRequest...创建方法
            - `alloc / initWithRequest:delegate:`需要手动调用 start 开启网络请求
            - `alloc / initWithRequest:delegate:startImmediately:`根据最后一个参数是否马上开启, 如果为 YES, 则马上自行开启网络请求, 如果为 NO 则也是要手动调用 start 
    - **（4）可以设置代理方法在哪个线程中执行**
        - `- setDelegateQueue:`对象方法, 设置这只代理在哪个线程中执行;
        - 默认情况下，代理方法会在主线程中进行调用（为了方便开发者拿到数据后处理一些刷新UI的操作不需要考虑到线程间通信）
    - **（5）遵守NSURLConnectionDataDelegate协议，并实现相应的代理方法, 在代理方法中监听网络请求的响应**
        - `- (void)connection:didReceiveResponse:`当接收到响应的时候调用
        - `- (void)connection:didReceiveData:`当接收到服务器返回数据的时候调用,**可能会调用多次**
        - `- (void)connection:didFailWithError:`当请求失败的时候调用该方法
        - `- (void)connectionDidFinishLoading:`当请求完成的时候调用该方法


- **注意: **
    - 数据有可能是比较多, 需要拼接数据, 所以这里就要定义的的是可变的数据
    -  `@property (strong, nonatomic) NSMutableData *resultData;`


- **异步请求（GET-代理）代码**

  ```objc
  //NSURLConnection异步请求（GET-代理）
  -(void)sendAsyncDelegate
  {
      //1.请求路径
      NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/login?username=520it&pwd=111&type=JSON"];

      //2.创建请求对象
      NSURLRequest *request = [NSURLRequest requestWithURL:url];

      //3.设置代理,主动自动发送请求
      // 注意: 这里只是简单的网络请求接收数据, 所以我们只要遵循<NSURLConnectionDataDelegate> 这个协议,
      // 注意: 实际是有多个相似的代理协议不要写错了,  <NSURLConnectionDataDelegate>
      // 设置代理的方法有两个
      // 方法一:需要手动开启发送网络请求
      //NSURLConnection *connect = [[NSURLConnection alloc]initWithRequest:request delegate:self];

      // 方法二: 最后一个参数决定是否自动发送网络请求
      //startImmediately YES 就和上面的方法没有区别, 会自动发送请求 也就是不需要手动调用 start 方法
      //                 NO  那么并不会发送请求,需要主动调用start方法
      NSURLConnection *connect = [[NSURLConnection alloc]initWithRequest:request delegate:self startImmediately:NO];

      //4.设置代理方法的执行队列
      //说明：默认情况下，代理方法会在主线程中进行调用（为了方便开发者拿到数据后处理一些刷新UI的操作不需要考虑到线程间通信）

      [connect setDelegateQueue:[[NSOperationQueue alloc]init]];
      //5.开始发送网络请求
      [connect start];

      //[connect cancel];//取消当前的网络请求
  }
  ```


- **设置代理的3种方法**

  ```objc
  //设置代理的第一种方式：使用类方法设置代理，会自动发送网络请求
  NSURLConnection *conn = [NSURLConnection connectionWithRequest:request delegate:self];
  //取消网络请求
  //[conn cancel];
  ```
  ```objc
  // 设置代理的第二种方式：自动发送网络请求
  NSURLConnection *connect = [[NSURLConnection alloc]initWithRequest:request delegate:self];
  ```
  ```objc
  // 设置代理的第三种方式：
  /*
  第一个参数：请求对象
  第二个参数：谁成为NSURLConnetion对象的代理
  第三个参数：是否马上发送网络请求，
            如果该值为YES则立刻发送，
            如果为NO则不会发送网路请求, 需要手动调用 start 方法
  */
  NSURLConnection *conn = [[NSURLConnection alloc]initWithRequest:request delegate:self startImmediately:NO];

  //调用该方法控制网络请求的发送
  [conn start];
  ```


- **相关的代理方法**

  ```objc
  /*
   1.当接收到服务器响应的时候调用
   第一个参数connection：监听的是哪个NSURLConnection对象
   第二个参数response：接收到的服务器返回的响应头信息
   */
  -(void)connection:(NSURLConnection *)connection didReceiveResponse:(NSURLResponse *)response
  {
      self.resultData = [NSMutableData data];
      NSLog(@"didReceiveResponse");
  }
  ```
  ```objc
  /*
   2.当接收到数据的时候调用，该方法会被调用多次
   第一个参数connection：监听的是哪个NSURLConnection对象
   第二个参数data：本次接收到的服务端返回的二进制数据（可能是片段）
   */
  - (void)connection:(nonnull NSURLConnection *)connection didReceiveData:(nonnull NSData *)data{
      NSLog(@"didReceiveData--%zd",data.length);
      //注意: 数据有可能是比较多, 需要拼接数据, 所以这里就要定义的的是可变的数据
      //@property (strong, nonatomic) NSMutableData *resultData;
      // 拼接服务器返回的数据, 如果是大数据, 比如视频文件, 则就直接写入到沙盒中, 避免造成应用占用内存过大
      [self.resultData appendData:data];
  }
  ```
  ```objc
  /*3.当请求错误的时候调用（比如请求超时）
   第一个参数connection：NSURLConnection对象
   第二个参数：网络请求的错误信息，如果请求失败，则error有值
   */
  - (void)connection:(nonnull NSURLConnection *)connection didFailWithError:(nonnull NSError *)error{
      NSLog(@"didFailWithError");
  }
  ```
  ```objc
  /*
   4.当服务端返回的数据接收完毕之后会调用
   通常在该方法中解析服务器返回的数据
   */
  -(void)connectionDidFinishLoading:(nonnull NSURLConnection *)connection{
      NSLog(@"connectionDidFinishLoading");
      NSLog(@"%@",[[NSString alloc]initWithData:self.resultData encoding:NSUTF8StringEncoding]);
  }
  ```

---
<br/>
##4. NSURLConnection发送POST请求
- **发送POST请求步骤**
    - **(1) 确定URL路径**
    - **(2) 创建请求对象（可变对象 NSMutableURLRequest）**
        - **注意: **只有在可变对象才能修改请求对象的请求方法
    - **(3) 设置请求体对象**
        - `HTTPMethod`属性, 修改请求对象的方法为POST<必须大写>
        - 设置请求头部信息
        - `timeoutInterval`属性, 请求响应等待时间(一般是15s)
    - **(4) 设置请求体(参数)**
        - `HTTPBody`属性, 设置请求体信息
        - 字符串转为(二进制)编码格式 
        - `type=JSON` 可以不传, 不传默认就是 `JSON` 格式, 开发中最好都写上
    - **(5) 发送请求(异步)**
        - 同步和异步各自只有一个类方法, 发送请求
        - `[NSURLConnection sendAsynchronousRequest: queue: completionHandler:]`
        - 该方法第二个参数: 队列,只是决定后面的第三个参数 block块, 在哪个线程中回调
    - **(6) 解析数据(解析的是响应体 `data` 的数据) 将二进制数据转字符串**
    - **补充**：设置请求超时，处理错误信息，设置请求头（如获取客户端的版本等等,请求头是可设置可不设置具体根据需求文档）


- **相关代码**

  ```objc
  -(void)post
  {
      /*
       GET:http://120.25.226.186:32812/login?username=520it&pwd=520&type=JSON
           协议头+主机地址+接口名称+?+参数1&参数2&参数3
       POST:http://120.25.226.186:32812/login
           协议头+主机地址+接口名称
       */

      //1.确定请求路径
      NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/login"];

      //2.创建可变请求对象
      // 注意: 这里要使用的是可变的请求对象,
      NSMutableURLRequest *request = [[NSMutableURLRequest alloc]initWithURL:url];

      //3 修改请求方法为POST<必须大写>
      request.HTTPMethod = @"POST";

      //3.1 设置请求对象
      // 该请求发送出去15秒之内如果还没有得到响应那么就认为请求失败
      request.timeoutInterval = 15;

      //3.2 设置请求头信息
      // User-Agent 用来收集客户端环境信息, 主要是给后台用的
      [request setValue:@"iOS 10.1" forHTTPHeaderField:@"User-Agent"];
      //  除了这个之外, 还有很多可以设置 HTTP 头部信息的内容 在笔记<<2-5 HTTP报文首部信息.pages>>中有相关的内容    

      //4.设置请求体(参数)  字符串转为(二进制)编码格式 (type=JSON 可以不传)
      request.HTTPBody = [@"username=520it&pwd=520it&type=JSON" dataUsingEncoding:NSUTF8StringEncoding];
      // 编码格式百分之九十九都是 NSUTF8StringEncoding 格式

      //5.发送请求(异步)
      //  这是个异步函数, 会开个子线程发送请求
      //  第二个参数: 队列  只是决定后面的 block 块, 在回调的时候在哪个线程中回调
  //    [NSURLConnection sendAsynchronousRequest:request queue:[[NSOperationQueue alloc]init] completionHandler:^(NSURLResponse * _Nullable response, NSData * _Nullable data, NSError * _Nullable connectionError) {   
  //        NSLog(@"%@",[NSThread currentThread]);

  //        //6.解析数据(解析的是响应体的数据) 将二进制数据转字符串
  //        NSLog(@"%@",[[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding]);
  //        
  //    }];

      [NSURLConnection sendAsynchronousRequest:request queue:[NSOperationQueue mainQueue] completionHandler:^(NSURLResponse * _Nullable response, NSData * _Nullable data, NSError * _Nullable connectionError) {

          NSLog(@"%@",[NSThread currentThread]);
          //6.解析数据 将二进制数据转字符串
          NSLog(@"%@",[[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding]); 
      }];
  }
  ```


---
<br/>
##5. URL中文转码问题

- URL是不支持中文, 因此如果URL字符串中包含中文那么在发送请求之前需要对URL进行中文转码
- 注意浏览器中的 http 的链接有时候可以看到有中文, 其实URL内部已经做了转码处理
- 如何对URL进行转码：`stringByAddingPercentEscapesUsingEncoding`

- **建议**:不管有没有中文字符, 都写上转码, 这样扩展性比较好

  ```objc
  -(void)get
  {
      //http://120.25.226.186:32812/login2?username=%E5%B0%8F%E7%A0%81%E5%93%A5&pwd=520it&type=JSON
      // NSString *urlStr = @"http://120.25.226.186:32812/login2?username=%E5%B0%8F%E7%A0%81%E5%93%A5&pwd=520it&type=JSON";

      // 建议在开发中都多写一步转码操作

      // url 是不支持中文, 因此当字符串中包含中文的时候需要转码
      // 有时候在浏览器的 url 上能看到有中文情况是因为浏览器做了处理, 发送的是转码后的的内容
      NSString *urlStr = @"http://120.25.226.186:32812/login2?username=小码哥&pwd=520it&type=JSON";

      // 打印转码前
      NSLog(@"start++++%@",urlStr);
      urlStr = [urlStr stringByAddingPercentEscapesUsingEncoding:NSUTF8StringEncoding];
      // 打印转码后
      NSLog(@"end++++%@",urlStr);

      //1.url
      NSURL *url = [NSURL URLWithString:urlStr];

      //2.创建请求对象
      NSURLRequest *request = [NSURLRequest requestWithURL:url];

      //3.发送请求
      [NSURLConnection sendAsynchronousRequest:request queue:[NSOperationQueue mainQueue] completionHandler:^(NSURLResponse * _Nullable response, NSData * _Nullable data, NSError * _Nullable connectionError) {

          if (connectionError) {
              NSLog(@"%@--",connectionError);
              return ;
          }
          //4.解析数据
          NSLog(@"%@",[[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding]);
      }];
  }
  ```
  ```objc
  -(void)post
  {
      //0.urlstr
      NSString *urlStr = @"http://120.25.226.186:32812/login2";

      //1.url
      NSURL *url = [NSURL URLWithString:urlStr];

      //2.创建请求对象
      NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];

      //2.1 修改请求方法为POST
      request.HTTPMethod = @"POST";

      //2.2 设置请求体
      request.HTTPBody = [@"username=小码哥&pwd=520it&type=JSON" dataUsingEncoding:NSUTF8StringEncoding];

      //3.发送请求
      [NSURLConnection sendAsynchronousRequest:request queue:[NSOperationQueue mainQueue] completionHandler:^(NSURLResponse * _Nullable response, NSData * _Nullable data, NSError * _Nullable connectionError) {

          if (connectionError) {
              NSLog(@"%@--",connectionError);
              return ;
          }
          //4.解析数据
          NSLog(@"%@",[[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding]);
      }];
  }
  ```


---
<br/>

##6. NSURLConnection和Runloop（面试）


- **1. 两种为NSURLConnection设置代理方式的区别**
  ```objc
  //设置代理的第一种方式：使用类方法设置代理，会自动发送网络请求
  NSURLConnection *conn = [NSURLConnection connectionWithRequest:request delegate:self];
  //取消网络请求
  //[conn cancel];
  ```
  ```objc
  //第二种设置方式：
  //通过该方法设置代理，不会自动的发送请求
  // [[NSURLConnection alloc]initWithRequest:request delegate:self];

  //第三种设置方式：
  //设置代理，startImmediately为NO的时候，该方法不会自动发送请求 , 若为 YES 的时候, 该方法是会自动发送请求
  NSURLConnection *connect = [[NSURLConnection alloc]initWithRequest:request delegate:self startImmediately:NO];
  //手动通过代码的方式来发送请求
  //注意该方法内部会自动的把connect添加到当前线程的RunLoop中在默认模式下执行
  [connect start];
  ```

- **2. 如何控制代理方法在哪个线程调用**

  ```objc
  //说明：默认情况下，代理方法会在主线程中进行调用（为了方便开发者拿到数据后处理一些刷新UI的操作不需要考虑到线程间通信）
  //设置代理方法的执行队列, 这里 alloc/init 了一个新的队列则是在子线程执行
  [connect setDelegateQueue:[[NSOperationQueue alloc]init]];
  ```

- **3. 开子线程发送网络请求的注意点，适用于自动发送网络请求模式**

  ```objc
  //在子线程中发送网络请求-调用start方法发送
  -(void)createNewThreadSendConnect1
  {
      //1.创建一个非主队列
      NSOperationQueue *queue = [[NSOperationQueue alloc]init];

      //2.封装操作，并把任务添加到队列中执行
      [queue addOperationWithBlock:^{

          NSLog(@"%@",[NSThread currentThread]);
          //2-1.确定请求路径
          NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/login?username=dd&pwd=ww&type=JSON"];

          //2-2.创建请求对象
          NSURLRequest *request = [NSURLRequest requestWithURL:url];

          //2-3.使用NSURLConnection设置代理，发送网络请求
          NSURLConnection *connection = [[NSURLConnection alloc]initWithRequest:request delegate:self startImmediately:YES];

          //2-4.设置代理方法在哪个队列中执行，如果是非主队列，那么代理方法将再子线程中执行
          [connection setDelegateQueue:[[NSOperationQueue alloc]init]];

          //2-5.发送网络请求
          //注意：start方法内部会把当前的connect对象作为一个source添加到当前线程对应的runloop中
          //区别在于，如果调用start方法开发送网络请求，那么再添加source的过程中，如果当前runloop不存在
          //那么该方法内部会自动创建一个当前线程对应的runloop,并启动。
          
          // 上面的方法中已经设置了 startImmediately:YES , 内部已经调用了 start 方法, 所以不用再手动调用 start 方法
          //[connection start];
      }];
  }
  ```
  ```objc
  //在子线程中发送网络请求-自动发送网络请求
  -(void)createNewThreadSendConnect2
  {
      NSLog(@"-----");
      //1.创建一个非主队列
      NSOperationQueue *queue = [[NSOperationQueue alloc]init];

      //2.封装操作，并把任务添加到队列中执行
      [queue addOperationWithBlock:^{

          //2-1.确定请求路径
          NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/login?username=dd&pwd=ww&type=JSON"];

          //2-2.创建请求对象
          NSURLRequest *request = [NSURLRequest requestWithURL:url];

          //2-3.使用NSURLConnection设置代理，发送网络请求
          //注意：该方法内部虽然会把connection添加到runloop,但是如果当前的runloop不存在，那么不会主动创建。
          NSURLConnection *connection = [NSURLConnection connectionWithRequest:request delegate:self];

          //2-4.设置代理方法在哪个队列中执行，如果是非主队列，那么代理方法将再子线程中执行
          [connection setDelegateQueue:[[NSOperationQueue alloc]init]];
          // 为保证connection 通过类方法创建时会自动调用 start 方法, 下面必须创建当前的 runloop, 并开启 runloop
          //2-5 创建当前线程对应的runloop,并开启
         [[NSRunLoop currentRunLoop]run];
      }];
  }
  ```

---
<br/>