# NSOperation

---

##0. 本节知识点:
1. 基本概念
2. 实现步骤
3. NSOperation的基本使用
4. NSOperationQueue    
   1. NSOperationQueue的基本概念
   2. NSOperationQueue的基本使用
   3. NSOperationQueue的其它使用
   4. NSOperationQueue的线程间通信
   5. 依赖和监听

---

##1. 基本概念
- 回顾GCD|NSThread|pthread的特性
- NSOperation用来封装操作
- NSOperationQueue用来存放任务
- **注意:** 一定要两个配合使用NSOperation和NSOperationQueue才能实现多线程编程

---

##2. 实现步骤

- **NSOperation是个抽象类，并不具备封装操作的能力，必须使用它的 3 个子类**
    - NSInvocationOperation
    - NSBlockOperation
    - 自定义子类继承NSOperation，实现内部相应的方法


- **NSOperation和NSOperationQueue实现多线程的具体步骤**
    - 先将需要执行的操作封装到一个NSOperation对象中
    - 然后将NSOperation对象添加到NSOperationQueue中
    - 系统会自动将NSOperationQueue中的NSOperation取出来
    - 将取出的NSOperation封装的操作放到一条新线程中执行


---

##3. NSOperation的基本使用


- **NSInvocationOperation**
    - 封装操作
    - 开启操作
    - **注意**:
        - 默认情况下，调用了start方法后并不会开一条新线程去执行操作，而是在当前线程同步执行操作
        - 只有将NSOperation放到一个NSOperationQueue中，才会异步执行操作


- **NSBlockOperation**
    - 封装操作
    - 追加任务
    - 开启操作
    - **注意:**
        - 如果一个操作中有多个任务，那么会开子线程
        - 注意：追加的任务并非一定在子线程中处理
        - 注意：即是只要NSBlockOperation封装的操作数 > 1，就会异步执行操作


- **自定义NSOperation**
    - 创建自定义NSOperation
    - 开启任务
    - **注意:**
        - 实现: 重写内部的Main方法，说明start方法内部也是调用的main方法
        - 优点: 有利于代码的封装和复用


- **相关代码**

```objc
// NSInvocationOperation
- (void)invocation{
    // 1. 封装操作
    /*
     第一个参数:目标对象
     第二个参数:调用目标对象的方法
     第三个参数:给调用的方法的传参 没有参数则写 nil
     */
    NSInvocationOperation *op1 = [[NSInvocationOperation alloc]initWithTarget:self selector:@selector(download1) object:nil];
    NSInvocationOperation *op2 = [[NSInvocationOperation alloc]initWithTarget:self selector:@selector(download2) object:nil];
    NSInvocationOperation *op3 = [[NSInvocationOperation alloc]initWithTarget:self selector:@selector(download3) object:nil];

    // 2. 开启任务
    [op1 start];
    [op2 start];
    [op3 start];
    // 这里没有添加到队列中都不会创建新线程, 而且是同步执行
}
```
```objc
// NSBlockOperation
- (void)block{
    // 1. 封装任务
    NSBlockOperation *bOp1 = [NSBlockOperation blockOperationWithBlock:^{
        NSLog(@"1-----%@",[NSThread currentThread]);
    }];
    NSBlockOperation *bOp2 = [NSBlockOperation blockOperationWithBlock:^{
        NSLog(@"2-----%@",[NSThread currentThread]);
    }];
    NSBlockOperation *bOp3 = [NSBlockOperation blockOperationWithBlock:^{
        NSLog(@"3-----%@",[NSThread currentThread]);
    }];
    // 1.1 追加任务
    //当一个操作中的任务数据大于1的时候,就会开子线程并发执行任务,
    //并且是所有操作的任务也都有可能通过子线程执行, 也可能是通过主线程执行, 根据系统自己决定
    [bOp3 addExecutionBlock:^{
        NSLog(@"4--- %@",[NSThread currentThread]);
    }];
    [bOp1 addExecutionBlock:^{
        NSLog(@"5--- %@",[NSThread currentThread]);
    }];

    // 2. 开启任务
    [bOp1 start];
    [bOp2 start];
    [bOp3 start];
}
```
```objc
// 自定义NSOperation
- (void)custom{
    // 继承 NSOperation 类的自定义类, 如果只是 简单的重写了自定义类中的 main 方法是不会开新线程的
    // 1. 实例化一个自定义操作对象
    CDHOperation *op1 = [[CDHOperation alloc]init];
    op1.name = @"op1";
    CDHOperation *op2 = [[CDHOperation alloc]init];
    op2.name = @"op2";

    // 开启任务
    [op1 start];
    [op2 start];
}
```

---

##4. NSOperationQueue
####4.1 NSOperationQueue的基本概念
- 回顾GCD中的四种队列
- **NSOperation中的两种队列**: 主队列和非主队列的关系和区别
    - **主队列**: 通过`+mainQueue`获得，凡是放到主队列中的任务都将在主线程执行
    - **非主队列**: 直接`alloc init`出来的队列。非主队列同时具备了并发和串行的功能，通过设置最大并发数属性来控制任务是并发执行还是串行执行，如果不修改属性默认是并发队列, 属性值为(-1); 


####4.2 NSOperationQueue的基本使用
- NSInvocationOperation+非主队列
- NSBlockOperation+非主队列
    - 封装任务
    - 追加任务
    - 简便方法
- 自定义NSOperation+非主队列
- 注意: 把操作添加到队列中的方法内部会自动调用start方法


- **相关代码**

```objc
//1. NSInvocationOperation
- (void)invocationQueue
{
    /*
     GCD中的队列：
     串行队列：自己创建的，主队列
     并发队列：自己创建的，全局并发队列
     NSOperationQueue
     主队列：[NSOperationQueue mainqueue];凡事放在主队列中的操作都在主线程中执行
     非主队列：[[NSOperationQueue alloc]init]，并发和串行，默认是并发执行的
     */

    //1.创建队列
    NSOperationQueue *queue = [[NSOperationQueue alloc]init];

    //2.封装操作
    NSInvocationOperation *op1 = [[NSInvocationOperation alloc]initWithTarget:self selector:@selector(download1) object:nil];
    NSInvocationOperation *op2 = [[NSInvocationOperation alloc]initWithTarget:self selector:@selector(download2) object:nil];
    NSInvocationOperation *op3 = [[NSInvocationOperation alloc]initWithTarget:self selector:@selector(download3) object:nil];

    //3.把封装好的操作添加到队列中
    [queue addOperation:op1];
    [queue addOperation:op2];
    [queue addOperation:op3];
    // 注意: 这里不需在调用 start 方法 , 因为 addOperation 内部已经做了 start
}
```
```objc
//2. NSBlockOperation
- (void)blockQueue
{
    //1.创建队列
    NSOperationQueue *queue = [[NSOperationQueue alloc]init];

    //2.封装操作
    NSBlockOperation *op1 = [NSBlockOperation blockOperationWithBlock:^{
        NSLog(@"1----%@",[NSThread currentThread]);
    }];
    NSBlockOperation *op2 = [NSBlockOperation blockOperationWithBlock:^{
        NSLog(@"2----%@",[NSThread currentThread]);
    }];

    // 追加任务
    [op2 addExecutionBlock:^{
        NSLog(@"3----%@",[NSThread currentThread]);
    }];
    [op2 addExecutionBlock:^{
        NSLog(@"4----%@",[NSThread currentThread]);
    }];

    //3.添加操作到队列中
    [queue addOperation:op1];
    [queue addOperation:op2];

    //补充：简便方法
    [queue addOperationWithBlock:^{
        NSLog(@"5----%@",[NSThread currentThread]);
    }];

}
```

```objc
//3. 自定义NSOperation
-(void)customOperationQueue
{
    //1.创建队列
    NSOperationQueue *queue = [[NSOperationQueue alloc]init];

    //2.封装操作
    //  好处：1.信息隐蔽
    //       2.代码复用
    CDHOperation *op1 = [[CDHOperation alloc]init];
    CDHOperation *op2 = [[CDHOperation alloc]init];

    //3.添加操作到队列中
    [queue addOperation:op1];
    [queue addOperation:op2];
}      
```


####4.3 NSOperationQueue的其它使用
- **最大并发数**
    - 作用: 通过设置最大并发数可以控制队列是并发的还是串行的，如果大于1那么队列里面的任务并发执行
    - maxConcurrentOperationCount==3
        同一时间最多只能执行三个任务,当大于1的时候并发执行
    - maxConcurrentOperationCount==1
        队列里面的所有任务串行执行
    - 默认值
        默认值为-1，默认是一个并发队列(-1 在计算机中经常表示最大值, 这里同样表示最大值, 最大并发数, 具体多少根据系统 CPU 的使用率, 分配并发数)
- **队列的挂起**
    - 当为YES的时候表示暂停，当为NO的时候表示继续
    - 任务是有状态的，如等待执行，正在执行等，挂起操作只能挂起当前非处于执行状态的任务
- **队列的取消**
    - 内部调用了每个任务的取消方法
    - 取消是不可恢复的
    - 如果自定义NSOperation苹果官方的建议
        - 每执行完一段耗时操作之后就检查当前操作是否被取消
- **操作依赖和监听**
    - 同一个队列中的任务的依赖
    - 注意不要循环依赖，循环依赖的任务将不会被执行
    - 跨队列依赖
    - completionBlock



- **相关代码**

```objc
//创建队列
NSOperationQueue *queue = [[NSOperationQueue alloc]init];
self.queue = queue;
```
```objc
//1.设置最大并发数
//注意点：该属性需要在任务添加到队列中之前进行设置
//该属性控制队列是串行执行还是并发执行
//如果最大并发数等于1，那么该队列是串行的，如果大于1那么是并行的
//系统的最大并发数有个默认的值，为-1(在计算中经常用 -1 表示最大值)，如果该属性设置为0，那么不会执行任何任务
queue.maxConcurrentOperationCount = 2;
```
```objc
// 2. 暂停和恢复以及取消
// 2.1 设置暂停和恢复
//suspended属性设置为YES表示暂停，suspended设置为NO表示恢复
//暂停表示不继续执行队列中的下一个任务(当前正在执行的任务会被执行完成)，暂停操作是可以恢复的
if (self.queue.isSuspended) {
    self.queue.suspended = NO;
}else{
    self.queue.suspended = YES;
}
// 2.2 取消队列里面的所有操作
//     取消之后，当前正在执行的操作的下一个操作将不再执行(正在执行的操作会被执行完)，而且永远都不在执行，
//     就像后面的所有任务都从队列里面移除了一样, 并且取消操作是不可以恢复的
[self.queue cancelAllOperations];
```
```objc
// 3. 自定义NSOperation取消操作
-(void)main
{
    //耗时操作1
    for (int i = 0; i<1000; i++) {
        NSLog(@"任务1-%d--%@",i,[NSThread currentThread]);
    }
    NSLog(@"+++++++++++++++++++++++++++++++++");

    //苹果官方建议，每当执行完一次耗时操作之后，就查看一下当前队列是否为取消状态，如果是，那么就直接退出
    //好处是可以提高程序的性能
    if (self.isCancelled) {
        return;// 正常退出
    }

    //耗时操作2
    for (int i = 0; i<1000; i++) {
        NSLog(@"任务1-%d--%@",i,[NSThread currentThread]);
    }
    NSLog(@"+++++++++++++++++++++++++++++++++");
}
```
```objc
// 4. 操作依赖和监听
-(void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event
{
    //1.封装操作
    NSBlockOperation *op1 = [NSBlockOperation blockOperationWithBlock:^{
        for (NSInteger i =0; i<10; i++) {
            NSLog(@"1-%zd--%@",i,[NSThread currentThread]);
        }
    }];

    NSBlockOperation *op2 = [NSBlockOperation blockOperationWithBlock:^{
        for (NSInteger i =0; i<10; i++) {
            NSLog(@"2-%zd--%@",i,[NSThread currentThread]);
        }
    }];

    NSBlockOperation *op3 = [NSBlockOperation blockOperationWithBlock:^{
        for (NSInteger i =0; i<10; i++) {
            NSLog(@"3-%zd--%@",i,[NSThread currentThread]);
        }
    }];

    NSBlockOperation *op4 = [NSBlockOperation blockOperationWithBlock:^{
        NSLog(@"4---%@",[NSThread currentThread]);
    }];

    //操作监听
    op1.completionBlock = ^{
        NSLog(@"-----我已经准备好了,快来看我吧--%@",[NSThread currentThread]);
    };

    //2.创建队列
    NSOperationQueue *queue = [[NSOperationQueue alloc]init];

    //设置操作依赖
    //op1<op2<op4<op3 ---->
    //!!!!不能设置循环依赖(死锁--op1&op2 不会执行)
    //    [op2 addDependency:op1];
    //    [op1 addDependency:op2];
    [op1 addDependency:op2];
    [op2 addDependency:op4];
    [op4 addDependency:op3];
    // 操作依赖还可以跨队列依赖

    //3.添加操作到队列里面
    [queue addOperation:op1];
    [queue addOperation:op2];
    [queue addOperation:op3];
    [queue addOperation:op4];
}
```



####4.4 NSOperationQueue的线程间通信
- **开子线程下载图片回到主线程刷新UI**
- **下载并合成图片最后回到主线程刷新UI**

- **相关代码**

```objc
// 开子线程下载图片回到主线程刷新UI
-(void)download
{
    //1.开子线程下载图片
    NSOperationQueue *queue = [[NSOperationQueue alloc]init];

    //2.封装下载图片
    NSBlockOperation *download = [NSBlockOperation blockOperationWithBlock:^{
        //2.1 url
        NSURL *url = [NSURL URLWithString:@"http://wanzao2.b0.upaiyun.com/system/pictures/27666230/original/1439885921_500x500.png"];

        //2.data
        NSData *data = [NSData dataWithContentsOfURL:url];

        //3.转换格式
        UIImage *image = [UIImage imageWithData:data];

        NSLog(@"Download----%@",[NSThread currentThread]);

        //4.回到主线程刷新UI
        [[NSOperationQueue mainQueue] addOperationWithBlock:^{
            self.imageView.image = image;
            NSLog(@"UI----%@",[NSThread currentThread]);
        }];
    }];

    //3.添加操作到队列里
    [queue addOperation:download];
}
```

```objc
// 下载并合成图片最后回到主线程刷新UI
-(void)combie
{
    //1.开子线程下载图片
    NSOperationQueue *queue = [[NSOperationQueue alloc]init];

    //2.封装下载图片1
    NSBlockOperation *download1 = [NSBlockOperation blockOperationWithBlock:^{
        //2.1 url
        NSURL *url = [NSURL URLWithString:@"http://wanzao2.b0.upaiyun.com/system/pictures/27666230/original/1439885921_500x500.png"];

        //2.data
        NSData *data = [NSData dataWithContentsOfURL:url];

        //3.转换格式
       self.image1 = [UIImage imageWithData:data];

        NSLog(@"Download----%@",[NSThread currentThread]);
    }];

    //3.封装下载图片2
    NSBlockOperation *download2 = [NSBlockOperation blockOperationWithBlock:^{
        //2.1 url
        NSURL *url = [NSURL URLWithString:@"http://wanzao2.b0.upaiyun.com/system/pictures/26771697/original/c381285de3007ada.png"];

        //2.data
        NSData *data = [NSData dataWithContentsOfURL:url];

        //3.转换格式
        self.image2 = [UIImage imageWithData:data];

        NSLog(@"Download----%@",[NSThread currentThread]);
    }];

    //4.合成图片
    NSBlockOperation *combie = [NSBlockOperation blockOperationWithBlock:^{

        //1.开启上下文
        UIGraphicsBeginImageContext(CGSizeMake(200, 200));

        //2.画图1.2
        [self.image1 drawInRect:CGRectMake(0, 0, 200, 100)];
        [self.image2 drawInRect:CGRectMake(0, 100, 200, 100)];
        self.image1 = nil;
        self.image2 = nil;

        //3.得到图片
        UIImage *image = UIGraphicsGetImageFromCurrentImageContext();

        NSLog(@"combie----%@",[NSThread currentThread]);

        //4.关闭上下文
        UIGraphicsEndImageContext();

        //5. 回到主线程刷新 UI
        [[NSOperationQueue mainQueue] addOperationWithBlock:^{
            self.imageView.image = image;
            NSLog(@"UI----%@",[NSThread currentThread]);
        }];
    }];

    //5.设置依赖
    [combie addDependency:download1];
    [combie addDependency:download2];

    //6.添加操作到队列里
    [queue addOperation:download1];
    [queue addOperation:download2];
    [queue addOperation:combie];

    //kvo
    [download2 addObserver:self forKeyPath:@"isCancelled" options:NSKeyValueObservingOptionNew context:nil];
}
```

---
