# NSThread

---
###0. 本节知识点:

1. 基本使用
2. 线程间通信

---


###1. 基本使用
- **NSThread创建线程的三种方式**
    - alloc/init方式创建
    - 分离出子线程
    - 开启后台线程


- **alloc init方式创建**
    - 需要调用Start方法开启线程
    - 可以对线程进行更加详细的设置

  ```objectivec
  //第一种创建线程的方式：alloc init.
  //特点：需要手动开启线程，可以拿到线程对象进行详细设置
  //创建线程
  /*
    第一个参数：目标对象
    第二个参数：选择器，线程启动要调用哪个方法
    第三个参数：前面方法要接收的参数（最多只能接收一个参数，没有则传nil）
  */
  NSThread *thread = [[NSThread alloc]initWithTarget:self selector:@selector(run:) object:@"chendehao"];
  //启动线程
  [thread start];
  ```


- **分离出子线程**
    - 自动启动
    - 类方法，没有返回值，无法拿到返回对象因此无法进行更加详细的设置

  ```objectivec
  //第二种创建线程的方式：分离出一条子线程
  //特点：自动启动线程，无法对线程进行更详细的设置
  /*
   第一个参数：线程启动调用的方法
   第二个参数：目标对象
   第三个参数：传递给调用方法的参数
   */
  [NSThread detachNewThreadSelector:@selector(run:) toTarget:self withObject:@"我是分离出来的子线程"];
  ```


- **开启后台线程**
    - 自动启动
    - 无法对线程进行更加详细的设置

  ```objectivec
  //第三种创建线程的方式：后台线程
  //特点：自动启动县城，无法进行更详细设置
  [self performSelectorInBackground:@selector(run:) withObject:@"我是后台线程"];
  ```
  

- **属性设置**
    - 线程的名称
    - 线程的优先级
        - 取值范围0.0~1.0之间
        - 1.0为优先级最高
        - 默认的优先级为0.5

  ```objectivec
  //设置线程的名称
  thread.name = @"线程A";

  //设置线程的优先级,注意线程优先级的取值范围为0.0~1.0之间，1.0表示线程的优先级最高,如果不设置该值，那么理想状态下默认为0.5
  thread.threadPriority = 1.0;
  ```


--- 


###2. 线程间通信

- **如何下载网络图片**
    - 确定网络资源图片的url
    - 根据url把图片的二进制数据下载到本地
    - 把二进制数据转换为图片

  ```objectivec
  -(void)touchesBegan:(nonnull NSSet<UITouch *> *)touches withEvent:(nullable UIEvent *)event{
      //开启一条子线程来下载图片
      [NSThread detachNewThreadSelector:@selector(downloadImage) toTarget:self withObject:nil];
  }

  -(void)downloadImage
  {
      //1.确定要下载网络图片的url地址，一个url唯一对应着网络上的一个资源
      //  注意还要设置 配置文件 将取消对 http 头的不安全性
      NSURL *url = [NSURL URLWithString:@"http://p6.qhimg.com/t01d2954e2799c461ab.jpg"];

      //2.根据url地址下载图片数据到本地（二进制数据
      NSData *data = [NSData dataWithContentsOfURL:url];

      //3.把下载到本地的二进制数据转换成图片
      UIImage *image = [UIImage imageWithData:data];

      //4.回到主线程刷新UI
      //4.1 第一种方式
  //    [self performSelectorOnMainThread:@selector(showImage:) withObject:image waitUntilDone:YES];

      //4.2 第二种方式
  //    [self.imageView performSelectorOnMainThread:@selector(setImage:) withObject:image waitUntilDone:YES];

      //4.3 第三种方式
      [self.imageView performSelector:@selector(setImage:) onThread:[NSThread mainThread] withObject:image waitUntilDone:YES];
  }
  ```

- **获得代码段的执行时间**
    - ①使用NSDate date
    - ②使用CFTimeInterval  CFAbsoluteTimeGetCurrent()

  ```objectivec
  //第一种方法
  NSDate *start = [NSDate date];
  //2.根据url地址下载图片数据到本地（二进制数据）
  NSData *data = [NSData dataWithContentsOfURL:url];

  NSDate *end = [NSDate date];
  // 注意: 这里的时间计算使用到的方法
  NSLog(@"第二步操作花费的时间为%f",[end timeIntervalSinceDate:start]);
  ```
  ```objectivec
  //第二种方法
  CFTimeInterval start = CFAbsoluteTimeGetCurrent();
  NSData *data = [NSData dataWithContentsOfURL:url];

  CFTimeInterval end = CFAbsoluteTimeGetCurrent();
  NSLog(@"第二步操作花费的时间为%f",end - start);
  ```

- **线程间通信**
    - onThread
    - onMainThread
    - 简便方法

  ```objectivec
  //4.回到主线程刷新UI
  //4.1 第一种方式
  [self performSelectorOnMainThread:@selector(showImage:) withObject:image waitUntilDone:YES];
  ```
  ```objectivec
  //4.2 第二种方式
  [self.imageView performSelectorOnMainThread:@selector(setImage:) withObject:image waitUntilDone:YES];
  ```
  ```objectivec
  //4.3 第三种方式(简便方法)
  [self.imageView performSelector:@selector(setImage:) onThread:[NSThread mainThread] withObject:image waitUntilDone:YES];
  ```

---
<br/>