

文档讲解

> - 本节学习过程中遇到无法解决的问题可以在[课程问答区](https://coding.imooc.com/learn/qa/321.html)进行[提问](https://coding.imooc.com/learn/qa/321.html)，课程老师会对你进行帮助辅导；
> - 欢迎加入课程官方群：687196170 和讲师以及其他师兄弟们一起学习交流；

## 异步：Future与FutureBuilder实用技巧

- 什么是Future？
- Future的常见用法？
  - 获取Future的结果？
  - 捕获Future的异常？
  - 结合async，await？
  - future.whenComplete？
  - future.timeout？
- 什么是FutureBuilder？
- FutureBuilder常见的用法？

## 什么是Future？

`Future`表示在接下来的某个时间的值或错误，借助`Future`我们可以在Flutter实现异步操作。

> 它类似于ES6中的Promise，提供`then`和`catchError`的链式调用；

`Future`是`dart:async`包中的一个类，使用它时需要导入`dart:async`包，`Future`有两种状态：

- pending - 执行中；
- completed - 执行结束，分两种情况要么成功要么失败；

## Future的常见用法？

- 使用`future.then`获取future的值与捕获future的异常
- 结合`async`,`await`
- `future.whenComplete`
- `future.timeout`

### 使用`future.then`获取future的值与捕获future的异常

```
import 'dart:async';

Future<String> testFuture() {
//   throw new Error();
  return Future.value('success');
//   return Future.error('error');
}

main() {
  testFuture().then((s) {
    print(s);
  }, onError: (e) {
    print('onError:');
    print(e);
  }).catchError((e) {
    print('catchError:');
    print(e);
  });
}
```

> 如果`catchError`与`onError`同时存在，则会只调用`onError`；

**Future的then的原型：**

```dart
Future<R> then<R>(FutureOr<R> onValue(T value), {Function onError});
```

第一个参数会成功的结果回调，第二个参数`onError`可选表示执行出现异常。

[练一练](https://dartpad.dartlang.org/a1c357685c8141d6b28587dfee315839)

### 结合`async` `await`

`Future`是异步的，如果我们要将异步转同步，那么可以借助`async` `await`来完成。

```
import 'dart:async';

test() async {
  int result = await Future.delayed(Duration(milliseconds: 2000), () {
    return Future.value(123);
  });
  print('t3:' + DateTime.now().toString());
  print(result);
}

main() {
  print('t1:' + DateTime.now().toString());
  test();
  print('t2:' + DateTime.now().toString());
}
```

[练一练](https://dartpad.dartlang.org/50166d54277401e3ad324dd4d9fa8d6a)

### future.whenComplete

有时候我们需要在`Future`结束的时候做些事情，我们知道`then().catchError()`的模式类似于`try-catch`，`try-catch`有个`finally`代码块，而`future.whenComplete`就是`Future`的finally。

```dart
import 'dart:async';
import 'dart:math';

void main() {
  var random = Random();
  Future.delayed(Duration(seconds: 3), () {
    if (random.nextBool()) {
      return 100;
    } else {
      throw 'boom!';
    }
  }).then(print).catchError(print).whenComplete(() {
    print('done!');
  });
}
```

### future.timeout

完成一个异步操作可能需要很长的时间，比如：网络请求，但有时我们需要为异步操作设置一个超时时间，那么，如何为`Future`设置超时时间呢？

```dart
import 'dart:async';

void main() {
  new Future.delayed(new Duration(seconds: 3), () {
    return 1;
  }).timeout(new Duration(seconds: 2)).then(print).catchError(print);
}
```

运行上述代码会看到：`TimeoutException after 0:00:02.000000: Future not completed`。

[练一练](https://dartpad.dartlang.org/c545f19c614e75ae10ed044328720661)

## 什么是FutureBuilder？

`FutureBuilder`是一个将异步操作和异步UI更新结合在一起的类，通过它我们可以将网络请求，数据库读取等的结果更新的页面上。

### FutureBuilder的构造方法

```
FutureBuilder({Key key, Future<T> future, T initialData, @required AsyncWidgetBuilder<T> builder })
```

- `future`： Future对象表示此构建器当前连接的异步计算；
- `initialData`： 表示一个非空的Future完成前的初始化数据；
- `builder`： AsyncWidgetBuilder类型的回到函数，是一个基于异步交互构建widget的函数；

这个`builder`函数接受两个参数`BuildContext context` 与 `AsyncSnapshot<T> snapshot`，它返回一个widget。`AsyncSnapshot`包含异步计算的信息，它具有以下属性：

`connectionState` - 枚举ConnectionState的值，表示与异步计算的连接状态，ConnectionState有四个值：none，waiting，active和done；
`data` - 异步计算接收的最新数据；
`error` - 异步计算接收的最新错误对象；

AsyncSnapshot还具有`hasData`和`hasError`属性，以分别检查它是否包含非空数据值或错误值。

现在我们可以看到使用`FutureBuilder`的基本模式。 在创建新的FutureBuilder对象时，我们将Future对象作为要处理的异步计算传递。 在构建器函数中，我们检查connectionState的值，并使用AsyncSnapshot中的数据或错误返回不同的窗口小部件。

https://flutter-academy.com/async-in-flutter-futurebuilder/

## FutureBuilder的使用？

```dart
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

void main() => runApp(new MyApp());

class MyApp extends StatefulWidget {
  @override
  State<StatefulWidget> createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  String showResult = '';

  Future<CommonModel> fetchPost() async {
    final response = await http
        .get('http://www.devio.org/io/flutter_app/json/test_common_model.json');
    Utf8Decoder utf8decoder = Utf8Decoder(); //fix 中文乱码
    var result = json.decode(utf8decoder.convert(response.bodyBytes));
    return CommonModel.fromJson(result);
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Future与FutureBuilder实用技巧'),
        ),
        body: FutureBuilder<CommonModel>(
            future: fetchPost(),
            builder:
                (BuildContext context, AsyncSnapshot<CommonModel> snapshot) {
              switch (snapshot.connectionState) {
                case ConnectionState.none:
                  return new Text('Input a URL to start');
                case ConnectionState.waiting:
                  return new Center(child: new CircularProgressIndicator());
                case ConnectionState.active:
                  return new Text('');
                case ConnectionState.done:
                  if (snapshot.hasError) {
                    return new Text(
                      '${snapshot.error}',
                      style: TextStyle(color: Colors.red),
                    );
                  } else {
                    return new Column(children: <Widget>[
                      Text('icon:${snapshot.data.icon}'),
                      Text('statusBarColor:${snapshot.data.statusBarColor}'),
                      Text('title:${snapshot.data.title}'),
                      Text('url:${snapshot.data.url}')
                    ]);
                  }
              }
            }),
      ),
    );
  }
}

class CommonModel {
  final String icon;
  final String title;
  final String url;
  final String statusBarColor;
  final bool hideAppBar;

  CommonModel(
      {this.icon, this.title, this.url, this.statusBarColor, this.hideAppBar});

  factory CommonModel.fromJson(Map<String, dynamic> json) {
    return CommonModel(
      icon: json['icon'],
      title: json['title'],
      url: json['url'],
      statusBarColor: json['statusBarColor'],
      hideAppBar: json['hideAppBar'],
    );
  }
}
```

- https://flutter-academy.com/async-in-flutter-futurebuilder/

> - 本节学习过程中遇到无法解决的问题可以在[课程问答区](https://coding.imooc.com/learn/qa/321.html)进行[提问](https://coding.imooc.com/learn/qa/321.html)，课程老师会对你进行帮助辅导；
> - 欢迎加入课程官方群：687196170 和讲师以及其他师兄弟们一起学习交流；