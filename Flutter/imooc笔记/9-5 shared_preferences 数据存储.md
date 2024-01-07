在这篇文章中，我将向大家分享Flutter 本地存储的一些实用知识和技巧。首先会带你一起认识[什么是shared_preferences](https://coding.imooc.com/class/321.html)、[如何使用shared_preferences](https://coding.imooc.com/class/321.html)、以及[shared_preferences有那些常用的API？](https://coding.imooc.com/class/321.html)，最后会通过一个[计数器的例子](https://coding.imooc.com/class/321.html)来巩固Flutter 中本地存储的知识点等。

> - 在你学习Flutter 本地存储过程中遇到无法解决的问题或疑问，都可以在[课程问答区](https://coding.imooc.com/learn/qa/321.html)进行[提问](https://coding.imooc.com/learn/qa/321.html)，课程老师会对你进行辅导和帮助；

## 目录

- `shared_preferences` 是什么？
- 如何使用`shared_preferences `？
- `shared_preferences`有那些常用的API？
- 基于`shared_preferences`实现计数器Demo

数据存储是开发APP必不可少的一部分，比如页面缓存，从网络上获取数据的本地持久化等，那么在Flutter中如何进行数据存储呢？

> Flutter官方推荐我们用[shared_preferences](https://coding.imooc.com/class/321.html)进行数据存储，它类似于[React Native](https://coding.imooc.com/class/304.html)中的[`AsyncStorage`](https://coding.imooc.com/class/304.html)。

## 什么是shared_preferences?

[shared_preferences](https://coding.imooc.com/class/321.html)是Flutter社区开发的一个本地数据存取插件，它有以下特性：

- 简单的，异步的，持久化的key-value存储系统；
- 在Android上它是基于[SharedPreferences](https://coding.imooc.com/class/321.html)的；
- 在iOS上它是基于[NSUserDefaults](https://coding.imooc.com/class/321.html)的；

## 如何使用shared_preferences？

首先在[pubspec.yaml](https://coding.imooc.com/class/321.html)文件中添加：

```
dependencies:
  shared_preferences: ^0.5.1+
```

记得运行安装哦：[`flutter packages get`](https://coding.imooc.com/class/321.html)

在需要用到的文件中导入：

```
import 'package:shared_preferences/shared_preferences.dart';
```

> 存储数据

```
final prefs = await SharedPreferences.getInstance();

// set value
prefs.setInt('counter', counter);
```

> [查看全部完整代码](https://coding.imooc.com/class/321.html)。

> 读取数据

```
final prefs = await SharedPreferences.getInstance();

// Try reading data from the counter key. If it does not exist, return 0.
final counter = prefs.getInt('counter') ?? 0;}
```

> [查看全部完整代码](https://coding.imooc.com/class/321.html)。

> 删除数据

```
final prefs = await SharedPreferences.getInstance();
prefs.remove('counter');
```

> [查看全部完整代码](https://coding.imooc.com/class/321.html)。

## shared_preferences有那些常用的API？

### 存储相关

![shared_preferences](https://www.devio.org/io/flutter_app/img/blog/shared_preferences_set.png)

> 如上图`shared_preferences`支持[int](https://coding.imooc.com/class/321.html), [double](https://coding.imooc.com/class/321.html), [bool](https://coding.imooc.com/class/321.html), [string](https://coding.imooc.com/class/321.html) 与 [stringList](https://coding.imooc.com/class/321.html)类型的数据存储；

### 读取相关

![shared_preferences](https://www.devio.org/io/flutter_app/img/blog/shared_preferences_get.png)

> 上图[`shared_preferences`](https://coding.imooc.com/class/321.html)中所提供的读取相关的API；

## 基于shared_preferences实现计数器Demo

![shared_preferences](https://www.devio.org/io/flutter_app/img/blog/shared_preferences_demo.gif)

```
...
class _CounterWidget extends StatefulWidget {
  @override
  _CounterState createState() => _CounterState();
}

class _CounterState extends State<_CounterWidget> {
  String countString = '';
  String localCount = '';

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Column(
        children: <Widget>[
          RaisedButton(
              onPressed: _incrementCounter, child: Text('Increment Counter')),
          RaisedButton(onPressed: _getCounter, child: Text('Get Counter')),
          Text(
            countString,
            style: TextStyle(fontSize: 20),
          ),
          Text(
            'result：' + localCount,
            style: TextStyle(fontSize: 20),
          ),
        ],
      ),
    );
  }

  _incrementCounter() async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    setState(() {
      countString = countString + " 1";
    });
    int counter = (prefs.getInt('counter') ?? 0) + 1;
    await prefs.setInt('counter', counter);
  }

  _getCounter() async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    setState(() {
      localCount = prefs.getInt('counter').toString();
    });
  }
}
```

> [查看全部完整代码](https://coding.imooc.com/class/321.html)。

以上便是Flutter 本地存储的一些实用知识和技巧，你Get到了吗！

> - 本文学习过程中遇到无法解决的问题可以在[课程问答区](https://coding.imooc.com/learn/qa/321.html)进行[提问](https://coding.imooc.com/learn/qa/321.html)，课程老师会对你进行辅导和帮助；
> - 欢迎加入课程官方群：`795410523` 和讲师以及其他师兄弟们一起学习交流；

## [参考资料](https://coding.imooc.com/class/321.html)

- [Flutter高级进阶实战 仿哔哩哔哩APP](https://coding.imooc.com/class/487.html)
- [Flutter从入门到进阶实战携程网App](https://coding.imooc.com/class/321.html)