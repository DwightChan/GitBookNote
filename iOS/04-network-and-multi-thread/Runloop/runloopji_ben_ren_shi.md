# Runloop基本认识

<br/>

##0. 本节知识点:
1. 字面意思
2. 基本作用（作用重大）
3. 重要说明
4. Runloop对象
5. Runloop参考资料
6. Runloop与线程
7. Runloop运行原理图


--- 
<br/>


##1. 字面意思
- 运行循环
- 跑圈

---
<br/>

##2. 基本作用（作用重大）
- 保持程序的持续运行(ios程序能一直活着不会死)
- 处理app中的各种事件（比如触摸事件、定时器事件（NSTimer）、selector事件（performSelector）
- 节省CPU资源，提高程序性能，有事情就做事情，没事情就休息

---
<br/>
##3. 重要说明
- （1）如果没有Runloop,那么程序一启动就会退出，什么事情都做不了。
- （2）如果有了Runloop，那么相当于在内部有一个死循环，能够保证程序的持续运行
- （3）main函数中的Runloop
    - 在UIApplication函数内部就启动了一个Runloop，该函数返回一个int类型的值
    - 这个默认启动的Runloop是跟主线程相关联的

---
<br/>

##4. Runloop对象
- 在iOS开发中有两套api来访问Runloop,它们是等价的，可以互相转换,
    - foundation框架【NSRunloop】
    - core foundation框架【CFRunloopRef】
- NSRunLoop和CFRunLoopRef都代表着RunLoop对象,它们是等价的，可以互相转换
- NSRunLoop是基于CFRunLoopRef的一层OC包装，所以要了解RunLoop内部结构，需要多研究CFRunLoopRef层面的API（Core Foundation层面）
    - Foundation
        - [NSRunLoop mainRunLoop]；获得主线程对应的Runloop
        - [NSRunLoop currentRunLoop]；获得执行当前方法的线程对应的Runloop
    - CoreFoundation
        - CFRunLoopGetMain()；获得主线程对应的Runloop
        - CFRunLoopGetCurrent()；获得执行当前方法的线程对应的Runloop


- **相互转换**
    - CFRunLoopRef runloop = mainRunLoop.getCFRunLoop；


- **注意**: 虽然表示的是等价, 可以相互转换但是要通过转换之后打印的地址才会一样.


---
<br/>
##5. Runloop参考资料
- 苹果官方文档: [https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html)

- CFRunLoopRef开源代码下载地址：
[http://opensource.apple.com/source/CF/CF-1151.16/](http://opensource.apple.com/source/CF/CF-1151.16/)


---
<br/>
##6. Runloop与线程
- Runloop和线程的关系：一个Runloop对应着一条唯一的线程
    - 问题：如何让子线程不死
    - 回答：给这条子线程开启一个Runloop
- Runloop的创建：主线程Runloop已经创建好了，子线程的runloop需要手动创建
- Runloop的生命周期：在第一次获取时创建，在线程结束时销毁


---
<br/>
##7. Runloop运行原理图

<img src="../images/多线程/Runloop2.png" width="600" height="300">


---
<br/>

