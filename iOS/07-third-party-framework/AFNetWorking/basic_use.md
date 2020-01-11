# 基本使用(Basic use)
1. 发送 get 请求
2. 发送 post 请求
3. 文件下载
4. 文件上传

---
<br />

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