# NSURLSessionDownloadTask支持大文件下载


<br/>
##本节知识点:
1. 第一种方法, block 下载, 不能监听下载进度
2. 第二种方法, 代理下载, 可以监听下载进度


---
<br/>
##1. 第一种方法, block 下载, 不能监听下载进度
- 1）使用 NSURLSession 和 NSURLSessionDownloadTask 可以很方便的实现文件下载操作
- 2）downloadTaskWithURL 内部默认已经实现了变下载边写入操作，所以不用开发人员担心内存问题
- 3）文件下载后默认保存在 tmp 文件目录，需要开发人员手动的剪切到合适的沙盒目录, 如果不剪切到合适的沙盒目录中, 在 tmp 目录会不定时删除数据
- 4）缺点：没有办法监控下载进度


- **实现步骤:**
    - 确定请求路径
    - 创建请求对象
    - 创建 session 会话对象(获取单例对象)
    - 创建 DownloadTask , 是根据 session 会话对象调用 `downloadTaskWithRequest: completionHandler:`方法创建
        - `downloadTaskWithURL:`方法已经实现了在下载文件数据的过程中边下载文件数据，边写入到沙盒文件的操作, 但是不能再下载完成时回调解析数据因此不用此方法
        - `downloadTaskWithRequest: completionHandler:`方法已经实现了在下载文件数据的过程中边下载文件数据，边写入到沙盒文件的操作, 可以在回调中解析数据, 并将文件从 tmp 目录转移,避免被删除
    -  执行 task
    - 回调解析, 转移数据
        - **注意**:数据是存储在 temp 文件夹中随时都有可能被删除, 因此就要有下面的步骤
        - 剪切到安全的地方

- **缺点: 不能监听文件下载进度**


- **相关代码**

  ```objc
  //无法监听文件的下载进度
  -(void)downloadBlock
  {
      //1.确定请求路径
      NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/resources/videos/minion_01.mp4"];

      //2.创建请求对象
      NSURLRequest *request = [NSURLRequest requestWithURL:url];

      //3.创建会话对象
      NSURLSession *session = [NSURLSession sharedSession];

      //4.task
      /*
       第一个参数:location 临时存储路径
       第二个参数:response 响应头信息
       第三个参数:error 错误信息
       */
      //说明：downloadTaskWithRequest方法已经实现了在下载文件数据的过程中边下载文件数据，边写入到沙盒文件的操作
      NSURLSessionDownloadTask *downloadTask = [session downloadTaskWithRequest:request completionHandler:^(NSURL * _Nullable location, NSURLResponse * _Nullable response, NSError * _Nullable error) {

          // 打印文件临时存储路径, 随时会被删除, 根据路径可能已经找不到文件了, 是因为已经被删除
          NSLog(@"%@",location);
          /*
            file:///Users/apple/Library/Developer/CoreSimulator/Devices/493D8296-6BCE-4646-871A-B399533590AE/data/Containers/Data/Application/322FC5D9-8B95-4E53-81E3-5A3965D377DE/tmp/CFNetworkDownload_l5MBnn.tmp
           */
          //剪切到安全的地方
          //得到caches路径
          NSString *caches = [NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES) lastObject];
          // 根据响应的信息(属性)设置文件名称
          NSString *fileName = response.suggestedFilename;
          //拼接全路径
          NSString *fullPath = [caches stringByAppendingPathComponent:fileName];

          //剪切文件
          /*
           第一个参数:要剪切的文件在哪里 NSURL
           第二个参数:要剪切到什么地方 NSURL
           第三个参数:错误信息
           */
  //        [[NSFileManager defaultManager] moveItemAtPath:<#(nonnull NSString *)#> toPath:<#(nonnull NSString *)#> error:<#(NSError * _Nullable __autoreleasing * _Nullable)#>]

          [[NSFileManager defaultManager] moveItemAtURL:location toURL:[NSURL fileURLWithPath:fullPath] error:nil];

          // 打印剪切后的文件路径
          NSLog(@"%@",fullPath);

      }];

      //5.执行task
      [downloadTask resume];
  }
  ```


---
<br/>
##2. 第二种方法, 代理下载, 可以监听下载进度

- 1）创建NSURLSession并设置代理，通过NSURLSessionDownloadTask并以代理的方式来完成大文件的下载
- 2）常用代理方法的说明
- 3）实现断点下载相关代码
    - 开始下载
    - 暂停
    - 取消
    - 恢复
- 4）计算当前下载进度
- **5）局限性**
    - 如果用户点击暂停之后退出程序，那么需要把恢复下载的数据写一份到沙盒，代码复杂度大
    - 如果用户在下载中途未保存恢复下载数据即退出程序，则不具备可操作性


- **实现步骤**
    - 确定请求路径
    - 创建请求对象
    - 创建会话对象 session, 类方法创建
        - `sessionWithConfiguration:delegate:delegateQueue:`
        - 设置配置
        - 设置代理
        - 设置(代理方法的)执行队列
    - 创建下载任务 downloadTask , 通过会话对象 session
    - 执行任务
    - 遵循代理协议, 实现代理方法
        - 下载文件
        - 监听下载进度
        - 剪切文件到安全的地方


- **常用的代理方法**
    - `-(void)URLSession:downloadTask:didWriteData:totalBytesWritten:totalBytesExpectedToWrite:`
        - 写数据的时候调用, 可能会被调用很多次
    - `-(void)URLSession:downloadTask:didResumeAtOffset:expectedTotalBytes:`
        - (取消--继续下载)恢复下载的时候回调用
    - `-(void)URLSession:downloadTask:didFinishDownloadingToURL:`
        - 当下载完成的时候调用
    - `-(void)URLSession:task:didCompleteWithError:`
        - 当请求结束的时候调用


- **相关代码**

  ```objc
  //1）创建NSURLSession并设置代理，通过NSURLSessionDownloadTask并以代理的方式来完成大文件的下载
  //监听文件的下载进度
  -(void)downloadDelegate
  {
      //1.确定请求路径
      NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/resources/videos/minion_01.mp4"];

      //2.创建请求对象
      NSURLRequest *request = [NSURLRequest requestWithURL:url];

      //3.创建会话对象
      self.session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:self delegateQueue:[NSOperationQueue mainQueue]];

      //4.创建下载任务
      NSURLSessionDownloadTask *downloadTask = [self.session downloadTaskWithRequest:request];

      //5.执行TASK
      [downloadTask resume];
      // 属性引用
      self.downloadTask = downloadTask;
  }
  ```

- **< NSURLSessionDownloadDelegate > 代理方法 **

  ```objc
  #pragma mark -------------------
  #pragma mark NSURLSessionDownloadDelegate
  //1.写数据的时候调用, 可能会被调用很多次
  /*
   bytesWritten :本次下载数据的大小
   totalBytesWritten : 已经下载数据的总大小
   totalBytesExpectedToWrite :文件的总大小
   */
  -(void)URLSession:(NSURLSession *)session downloadTask:(NSURLSessionDownloadTask *)downloadTask didWriteData:(int64_t)bytesWritten totalBytesWritten:(int64_t)totalBytesWritten totalBytesExpectedToWrite:(int64_t)totalBytesExpectedToWrite{
      NSLog(@"当前已经下载了%f",1.0 * totalBytesWritten / totalBytesExpectedToWrite );
  }
  ```
  ```objc
  //2.(取消--继续下载)恢复下载的时候回调用
  /*
   2.恢复下载的时候调用该方法
   fileOffset:恢复之后，要从文件的什么地方开发下载
   expectedTotalBytes：该文件数据的总大小
   */
  -(void)URLSession:(NSURLSession *)session downloadTask:(NSURLSessionDownloadTask *)downloadTask didResumeAtOffset:(int64_t)fileOffset expectedTotalBytes:(int64_t)expectedTotalBytes{
      NSLog(@"didResumeAtOffset----");
  }
  ```
  ```objc
  //3.当下载完成的时候调用
  -(void)URLSession:(NSURLSession *)session downloadTask:(NSURLSessionDownloadTask *)downloadTask didFinishDownloadingToURL:(NSURL *)location{

      NSLog(@"%@",location);
      //1.得到caches路径
      NSString *caches = [NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES) lastObject];
      NSString *fileName = downloadTask.response.suggestedFilename;

      //2.拼接全路径
      NSString *fullPath = [caches stringByAppendingPathComponent:fileName];

      //3.剪切文件
      /*
       第一个参数:要剪切的文件在哪里 NSURL
       第二个参数:要剪切到什么地方 NSURL
       第三个参数:错误信息
       */
      [[NSFileManager defaultManager] moveItemAtURL:location toURL:[NSURL fileURLWithPath:fullPath] error:nil];
  }
  ```
  ```objc
  //4.当请求结束的时候调用
  // 如果请求失败，那么error有值
  -(void)URLSession:(NSURLSession *)session task:(NSURLSessionTask *)task didCompleteWithError:(NSError *)error{
      NSLog(@"didCompleteWithError");
  }
  ```

---
<br/>