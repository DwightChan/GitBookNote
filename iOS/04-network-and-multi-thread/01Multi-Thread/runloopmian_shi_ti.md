# RunLoop面试题

####1. 什么是RunLoop？
- 从字面意思看：运行循环、跑圈
- 其实它内部就是do-while循环，在这个循环内部不断地处理各种任务（比如Source、Timer、Observer）
- 一个线程对应一个RunLoop，主线程的RunLoop默认已经启动，子线程的RunLoop得手动启动（调用run方法）
- RunLoop只能选择一个Mode启动，如果当前Mode中没有任何Source(Sources0、Sources1)、Timer，那么就直接退出RunLoop

####2. 自动释放池什么时候释放？
- 通过Observer监听RunLoop的状态
- 第一次创建：Runloop启动的时候创建
- 最后一次销毁：Runloop退出的时候销毁
- 其它时候的创建和销毁：当Runloop即将进入休眠状态的时候会把当前的自动释放池释放并创建一个新的释放池


####3. 在开发中如何使用RunLoop？什么应用场景？
- 开启一个常驻线程（让一个子线程不进入消亡状态，等待其他线程发来消息，处理其他事件）
- 在子线程中开启一个定时器
- 在子线程中进行一些长期监控
- 可以控制定时器在特定模式下执行
- 可以让某些事件（行为、任务）在特定模式下执行
- 可以添加Observer监听RunLoop的状态，比如监听点击事件的处理（在所有点击事件之前做一些事情）