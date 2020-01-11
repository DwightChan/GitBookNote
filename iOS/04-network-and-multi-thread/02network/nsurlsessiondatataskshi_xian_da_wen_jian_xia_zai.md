# NSURLSessionDataTask实现大文件下载

<br/>
##本节知识点:
1. 应用需求
2. 基本思路
3. 关于`NSFileHandle`(文件句柄)的使用
4. 关于`NSOutputStream`(输出流)的使用
5. 关于网络请求请求头的设置（可以设置请求下载文件的某一部分）
6. 优化程序

--- 
<br/>
##1. 应用需求

- **需求与问题:**
    - 下载文件, 监听显示进度条
    - 解决下载内存飙升问题, 边下载数据边写入到沙盒(并且不会出现新数据覆盖旧数据, 而是数据拼接)
    - 断点下载, 暂停/取消或者退出之后, 下次启动下载能够继续上次下载的文件
    - 如何只下载一部分数据
    - 如何知道应该下载那部分数据


---
<br/>

##2. 基本思路


- **先暂时写死下载文件的存放路径 (宏定义路径)**
- **当程序驱动时**
    - 根据文件路径获得已经下载的文件大小
- **定义 `NSURLSessionDataTask *dataTask` 属性, 懒加载创建 task (网络请求下载任务)**
    - 确定请求路径
    - 创建请求对象
    - 设置请求首部字段, 实体的字节范围请求(Range), 从继续上一次下载点开始下载
    - 创建session
        - 设置代理
        - 设置配置
        - 设置代理方法添加到的队列
    - 创建task (根据 session 创建)


- **按钮控件的逻辑**
    - 开始
    - 暂停
    - 取消
        - 当用户取消下载任务的时候, 并 `self.dataTask = nil;` 释放内存
    - 恢复


- **通过对应的代理方法实现断点续传逻辑**
    - 1.当接收到服务器响应的时候调用`-(void)URLSession:dataTask:didReceiveResponse:completionHandler:`
        - 判断文件是否存在, 不存在则需要创建
        - 创建文件句柄或者输出流(用于后面的代理方法做断点续传)
        - **告诉代理接收数据**`completionHandler(NSURLSessionResponseAllow);`
    - 2.当接收到服务器返回数据的时候调用 可能会被调用多次`-(void)URLSession:dataTask:didReceiveData:`
        - 获取下载数据并计算文件下载进度
        - 断点续传(通过句柄或者输出流)
    - 3.当请求完成或者是失败的时候调用`-(void)URLSession: task:didCompleteWithError:`
        - 关闭和释放句柄/输出流,


- **注意: **
    - 这里代理方法在已经被设置在主线程调用, 因此 UI 刷新不用线程通信
    - 总的文件大小是要用本次期望下载文件的大小和上次已经下载的文件的相加


- **代码实现**

  ```objc
  //
  //  ViewController.m
  //  day05-10-掌握-NSURLSession文件下载(dataTask·开始暂停取消继续等常见操作)
  //
  //  Created by 陈德豪 on 16/6/24.
  //  Copyright © 2016年 陈德豪. All rights reserved.
  //
  ```
  ```objc
  #import "ViewController.h"

  #define KFileFullNamePath [[NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES)lastObject] stringByAppendingPathComponent:@"xiaohuangren.mp4"]

  @interface ViewController ()<NSURLSessionDataDelegate>
  @property (weak, nonatomic) IBOutlet UIProgressView *progressView;

  @property (nonatomic, strong) NSURLSessionDataTask *dataTask;
  @property (nonatomic, assign) NSUInteger currentSize;
  @property (nonatomic, assign) NSUInteger expectedContentLength;
  @property (nonatomic, strong) NSFileHandle *fileHandle;
  @property (nonatomic, strong) NSOutputStream *stream
  @end
  ```
  ```objc
  @implementation ViewController
  // 开始下载
  - (IBAction)start:(id)sender {
      [self.dataTask resume];
      NSLog(@"%s",__func__);
  }
  ```
  ```objc
  // 恢复下载
  - (IBAction)resume:(id)sender {
      [self.dataTask resume];
      NSLog(@"%s",__func__);
  }
  ```
  ```objc
  // 暂停下载
  - (IBAction)suspend:(id)sender {
      [self.dataTask suspend];

      // 修改完成部分的进度条的颜色为灰色
      self.progressView.tintColor = [UIColor grayColor];
      // 修改这个条的背景色
      //    self.progressView.trackTintColor = [UIColor grayColor];

      NSLog(@"%s",__func__);
  }
  ```
  ```objc
  // 取消下载
  - (IBAction)cancel:(id)sender {
      [self.dataTask cancel];
      self.dataTask = nil;
      NSLog(@"%s",__func__);
      // 修改进度条的颜色为灰色
      self.progressView.tintColor = [UIColor grayColor];
  }
  ```
  ```objc
  - (void)viewDidLoad {
      [super viewDidLoad];
  //    [[NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES)lastObject] stringByAppendingPathComponent:@"xiaohuangren.mp4"];

      // 获取已经下载的文件数据的大小
      NSDictionary *fileInfo = [[NSFileManager defaultManager]attributesOfItemAtPath:KFileFullNamePath error:nil];
      self.currentSize = [fileInfo fileSize];

      NSLog(@"%zd",self.currentSize);
      NSLog(@"%@",KFileFullNamePath);
  }
  ```
  ```objc
  // 懒加载创建下载任务
  - (NSURLSessionDataTask *)dataTask{
      if (!_dataTask) {
          // 1.确定请求路径
          NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/resources/videos/minion_02.mp4"];

          // 2. 创建请求
          //        NSURLRequest *request = [[NSURLRequest alloc]initWithURL:url];
          NSMutableURLRequest *request = [[NSMutableURLRequest alloc]initWithURL:url];

          // 3. 设置请求头部字段
          /*
           bytes=0-100    请求0-100
           bytes=200-1000
           bytes=200-     从200开始知道结尾
           bytes=-100
           */
          NSString *rangeStr = [NSString stringWithFormat:@"bytes=%zd-",self.currentSize];
          [request setValue:rangeStr forHTTPHeaderField:@"Range"];

          // 4. 创建会话session,设置代理
          /*
           第一个参数:配置信息 defaultSessionConfiguration
           第二个参数:self 成为代理
           第三个参数:队列 控制的是代理方法在哪个线程中调用
           */
          //delegateQueue nil 代理方法默认是在子线程执行的
          NSURLSession *session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:self delegateQueue:[[NSOperationQueue alloc] init]];

          // 5. 根据会话创建一个 task
          _dataTask = [session dataTaskWithRequest:request];
      }
      return _dataTask;
  }
  ```

- **代理方法--业务逻辑**

  ```objc
  #pragma mark - NSURLSessionDataDelegate
  // 1. 当接收到服务器响应的时候调用的代理方法 (只来一次)
  - (void)URLSession:(NSURLSession *)session dataTask:(NSURLSessionDataTask *)dataTask didReceiveResponse:(NSURLResponse *)response completionHandler:(void (^)(NSURLSessionResponseDisposition))completionHandler{

      // 获取请求数据的期望大小
      self.expectedContentLength = response.expectedContentLength + self.currentSize;
      /*
      // 方法一: 使用句柄拼接断点续传
      // 判断之前是否已经有过文件下载 ,没有则创建出来一个空的文件
      if (self.currentSize == 0) {
          // 创建一个新的文件
          [[NSFileManager defaultManager]createFileAtPath:KFileFullNamePath contents:nil attributes:nil];
      }
      // 创建文件句柄
      self.fileHandle = [NSFileHandle fileHandleForWritingAtPath:KFileFullNamePath];
      // 补充有时候我们记录用户上一次观看视频的到哪个点 就用下面这个方法
      //    [NSFileHandle fileHandleForReadingAtPath:KFileFullNamePath];

      // 将文件句柄移到文件的末尾
      [self.fileHandle seekToEndOfFile];
      */

      //方法二: 使用输出流拼接断点续传
      //1 关于NSOutputStream的使用
      //1. 创建一个输入流,数据追加到文件的屁股上
      //把数据写入到指定的文件地址，如果当前文件不存在，则会自动创建
      self.stream = [[NSOutputStream alloc]initToFileAtPath:KFullPath append:YES];
      //2. 打开流
      [self.stream open];

      //需要我们告诉系统应该如何处理服务器返回的数据
      /*
       NSURLSessionResponseCancel = 0,   取消请求,默认做法
       NSURLSessionResponseAllow = 1,   接收数据
       NSURLSessionResponseBecomeDownload = 2,   编程下载请求
       NSURLSessionResponseBecomeStream 变成流
       */
      // 告诉代理接收数据
      completionHandler(NSURLSessionResponseAllow);
  }
  ```
  ```objc
  // 2. 当接收到服务器返回数据的时候调用 可能会被调用多次
  - (void)URLSession:(NSURLSession *)session dataTask:(NSURLSessionDataTask *)dataTask didReceiveData:(NSData *)data{
      // 先将文件写入磁盘
      // 方法一: 使用句柄拼接断点续传
      //[self.fileHandle writeData:data];
      //方法二: 使用输出流拼接断点续传
      [self.stream write:data.bytes maxLength:data.length];

      // 计算进度
      self.currentSize += data.length;
      dispatch_async(dispatch_get_main_queue(), ^{
          float progess = 1.0 * self.currentSize / self.expectedContentLength;
          [self.progressView setProgress:progess animated:YES];
  //        self.progressView.progress = 1.0 * self.currentSize / self.expectedContentLength;
      });
      NSLog(@"%f",self.progressView.progress);
  }
  ```
  ```objc
  // 3. 当请求完成或者失败的时候会调用这个方法
  - (void)URLSession:(NSURLSession *)session task:(NSURLSessionTask *)task
  didCompleteWithError:(nullable NSError *)error{
      /*
      // 方法一: 使用句柄拼接断点续传
      // 关闭文件句柄
      [self.fileHandle closeFile];
      // 清空句柄的缓存
      self.fileHandle = nil;
      */
      //方法二: 使用输出流拼接断点续传
      [self.stream close]
      self.stream = nil;
  }
  @end
  ```


---
<br/>

##3. 关于`NSFileHandle`(文件句柄)的使用

- **一般要和`NSFileManager`类配合使用**
    - 判断是否已经有文件, 如果没有则根据要保存的文件全路径创建一个空文件`NSFileManager`
        - 参数: 1.传保存路径, 2.内容为空, 3.属性特性为空
- 根据要保存的文件全路径创建文件句柄`NSFileHandle`
    - 通过文件句柄拼控制写入磁盘的位置达到拼接文件,新数据不会覆盖旧数据
- 将文件句柄指针指向文件的末尾 `- seekToEndOfFile`
- 通过文件句柄写数据`- writeData:`
- 关闭文件句柄 `- closeFile`
- 释放文件句柄 `= nil;`

  ```objc
  #define KFileFullNamePath [[NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES)lastObject] stringByAppendingPathComponent:@"xiaohuangren.mp4"]
  @property (assign, nonatomic) NSInteger currentSize;
  @property (nonatomic, strong) NSFileHandle *fileHandle;
  ```
  ```objc
  // 使用句柄拼接文件实现断点续传
  // 判断之前是否已经有过文件下载 ,没有则创建出来一个空的文件
  if (self.currentSize == 0) {
      // 创建一个新的文件
      [[NSFileManager defaultManager]createFileAtPath:KFileFullNamePath contents:nil attributes:nil];
  }
  // 创建文件句柄
  self.fileHandle = [NSFileHandle fileHandleForWritingAtPath:KFileFullNamePath];

  // 将文件句柄移到文件的末尾
  [self.fileHandle seekToEndOfFile];

  // 先将文件写入磁盘
  [self.fileHandle writeData:data];

  // 关闭文件句柄
  [self.fileHandle closeFile];
  // 清空句柄的缓存
  self.fileHandle = nil;
  ```


##4. 关于NSOutputStream的使用

- **1 关于NSOutputStream的使用**

  ```objc
  //1. 创建一个输入流,数据追加到文件的屁股上
  /*
   第一个参数:指向的路径 如果该路径下面文件不存在那么会自动创建一个空的
   第二个参数:YES 表示把数据追加到文件的屁股上
   */
  NSOutputStream *stream = [[NSOutputStream alloc]initToFileAtPath:KFullPath append:YES];

  //2. 打开流
  [stream open];

  //3. 写入流数据 
  //   注意: 第一个参数接收的是字节
  [stream write:data.bytes maxLength:data.length];

  //4.当不需要的时候应该关闭流
  [stream close];
  ```

--- 
<br/>
##5. 关于网络请求请求头的设置（可以设置请求下载文件的某一部分）

- 

  ```objc
  //1. 设置请求对象
  //1.1 创建请求路径
  NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/resources/videos/minion_01.mp4"];

  //1.2 创建可变请求对象
  NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];

  //1.3 拿到当前文件的残留数据大小
  self.currentContentLength = [self FileSize];

  //1.4 告诉服务器从哪个地方开始下载文件数据
  NSString *range = [NSString stringWithFormat:@"bytes=%zd-",self.currentContentLength];
  NSLog(@"%@",range);

  //1.5 设置请求头
  [request setValue:range forHTTPHeaderField:@"Range"];
  ```


--- 
<br/>




##6. 优化程序
- 关于文件下载进度的实时更新


- 程序重启是能显示上次进度
    - 下载进度与总的期望数据写入沙盒
    - 程序启动时尝试加载沙盒数据显示上一次下载进度


- 已经下完成,则在次点击下载则不发请求


- 方法的独立与抽取
    - 提供 session 属性, 懒加载


- session 设置代理要注意避免内存泄漏
    - session 会对代理进行强引用, 会造成内存泄漏
    - 这里是设置了控制为 session 的代理, 在所以在控制器 view 被释放的时候要对 session 的代理释放
    - **注意: 不能再 dealloc 方法中移除 session 的代理, 必须在`viewDidDisappear`方法中移除 session 代理**

  ```objc
  // 程序已启动就加载沙盒中的数据, 刷新进度条
  //获得已经下载的文件数据的大小
  NSDictionary *fileInfo =  [[NSFileManager defaultManager] attributesOfItemAtPath:KFullPath error:nil];
  NSLog(@"%@",fileInfo);

  //[fileInfo fileSize]
  NSInteger currentSize = [fileInfo[@"NSFileSize"] integerValue];
  self.currentSize = currentSize;

  //尝试获得文件的总大小(1之前没有下载过2之前已经下载过)
  NSData *data = [NSData dataWithContentsOfFile:KTotalSizeFullPath];
  if (data) {
      NSInteger totalSzie = [[[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding] integerValue];

      //计算文件的下载进度
      if (self.currentSize == 0) {// 什么不做
      }else {
          self.progressView.progress = 1.0 * self.currentSize / totalSzie;
      }
  }
  ```
  ```objc
  //判断文件是否已经下载完成,如果已经下载完成那么久不再发生请求
  if(self.progressView.progress == 1)
  {
      NSLog(@"该文件已经下载完成,可以直接使用");
      return nil;
  }     
  ```
  ```objc
  #pragma mark -------------------
  #pragma mark lazy loading
  -(NSURLSession *)session
  {
      if ( !_session ) {
          //3.创建session,设置代理
          /*
           第一个参数:配置信息 defaultSessionConfiguration
           第二个参数:self 成为代理
           第三个参数:队列 控制的是代理方法在哪个线程中调用
           */
          //delegateQueue nil 代理方法默认是在子线程执行的
          _session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:self delegateQueue:[NSOperationQueue mainQueue]];
      }
      return _session;
  }
  ```

  ```objc
  -(void)viewDidDisappear:(BOOL)animated{
      [super viewDidDisappear:animated];
      [self.session invalidateAndCancel]; //释放代理对象
  }
  ```
  ```objc
  -(void)dealloc
  {
      //在最后的时候应该把session释放，以免造成内存泄露
      //    NSURLSession设置过代理后，需要在最后（比如控制器销毁的时候）调用session的invalidateAndCancel或者resetWithCompletionHandler，才不会有内存泄露
      //    [self.session invalidateAndCancel];
      [self.session resetWithCompletionHandler:^{

          NSLog(@"释放---");
      }];
  }
  ```

---
<br/>