


# 11-2 Flutter混合开发流程与创建Flutter module

1. 创建 flutter module 
2. 添加 flutter module 依赖
3. 在原生项目调用 flutter
4. 编写 dart 代码


[Flutter与Android混合开发
](https://coding.imooc.com/learn/questiondetail/150166.html)

[Flutter与iOS混合开发](
https://coding.imooc.com/learn/questiondetail/150168.html)

[Flutter与Android通信开发指南](https://coding.imooc.com/learn/questiondetail/135975.html)

[Flutter与iOS通信开发指南](https://coding.imooc.com/learn/questiondetail/159484.html)


# 11-7 Flutter通信机制&Dart端讲解

三种 Channel 
1. MethodChannel 的Dart端实现
    1. MethodChannel 简单通信
    2. 原生端响应Dart调用
2. BasicMessageChannel 的Dart端实现
3. EventChannel 的Dart端实现

- **注意**
  - 使用原生 交互 需要用 window 在 dart:ui 包中 带有，
  - 在event Channel初始化的时候会返回 StreamSubscription 类型的对象，该对象在`dispose` 方法中 需要调用 `cancel` 方法释放资源；


通讯 中间 使用 编解码器
