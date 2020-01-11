# NSFileHandle & NSOutputStream

<br/>

##本节知识点:
1. 关于`NSFileHandle`(文件句柄)的使用
2. 关于`NSOutputStream`(输出流)的使用


---
<br/>

##1. 关于`NSFileHandle`(文件句柄)的使用

- **一般要和`NSFileManager`类配合使用**
    - 判断是否已经有文件, 如果没有则根据要保存的文件全路径创建一个空文件`NSFileManager`
        - 参数: 1.传保存路径, 2.内容为空, 3.属性特性为空
- 根据要保存的文件全路径创建文件句柄`NSFileHandle`
    - 通过文件句柄拼控制写入磁盘的位置达到拼接文件,新数据不会覆盖旧数据
- 将文件句柄指针指向文件的末尾, 对象方法 `-seekToEndOfFile`
- 通过文件句柄写数据, 对象方法`-writeData:`
- 关闭文件句柄, 对象方法`-closeFile`
- 释放文件句柄`self.handle = nil;`

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
  
  
  ---
  <br/>


##2. 关于`NSOutputStream`(输出流)的使用

- **顾名思义: 指定数据的流向**

  ```objc
  #define KFileFullNamePath [[NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES)lastObject] stringByAppendingPathComponent:@"xiaohuangren.mp4"]
  ```
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
  //    NSData *data = [[NSData alloc]init];
  NSData *datat = [NSData data];
  // 这里只是伪造了个 data 方便理解, 一般情况这里的 data 会是文件下载的代理方法中提供的直接获取
  //   注意: 第一个参数接收的是字节
  [stream write:data.bytes maxLength:data.length];

  //4.当不需要的时候应该关闭流
  [stream close];
  ```


  
  ---
  <br/>
