# phread的简单使用

---
##0. 本节知识点:

1. 简单介绍
2. 创建线程

---

##1. 简单介绍
- C语言的API,P是POSIX的简写,了解既可
    

---

##2. 创建线程
    
    
```objectivec
// 说明：pthread的基本使用（需要包含头文件）
#import <pthread.h>

//使用pthread创建线程对象
pthread_t thread;
NSString *name = @"wendingding";
//使用pthread创建线程
//第一个参数：线程对象地址
//第二个参数：线程属性 (名称\优先级)
//第三个参数：指向函数的指针
//第四个参数：传递给该函数的参数, 可以不传递
pthread_create(&thread, NULL, run, (__bridge void *)(name));
```


```objectivec
//知识点
/*
 1)线程内部多个任务是串行执行的
 2)NSThread获得当前线程,获得主线程,判断是否是主线程的3种方法
 3)耗时操作放在主线程中执行会卡住主线程,影响UI->解决方案:把耗时操作放在子线程中去执行
 */
- (void)test2{
    
    //1.当前的方法在哪个线程中执行
    //默认情况下,几乎所有的方法都是在主线程中执行的
    NSThread *currentThread = [NSThread currentThread];
    NSLog(@"%@",currentThread);
    
    //2.获得应用程序的主线程
    NSThread *mainThread = [NSThread currentThread];
    NSLog(@"%@",mainThread);
    
    //2.1 判断线程是否是主线程
    //1)number == 1 是主线程,否则就是子线程
    //2)类方法判断
    BOOL isMainThreadA = [NSThread isMainThread];
    NSLog(@"%d", isMainThreadA);
    
    //3)对象方法
    BOOL isMainThreadB = [currentThread isMainThread];
    NSLog(@"%d",isMainThreadB);
    
    //3.耗时(执行完该任务需要花费较多的时间)操作的执行
    //    for (NSInteger i = 0 ; i < 10000; i++) {
    //        NSLog(@"%zd---%@",i,[NSThread currentThread]);
    //    }
    
    //4.结论:耗时操作应该放到子线程中去执行
}
```

---