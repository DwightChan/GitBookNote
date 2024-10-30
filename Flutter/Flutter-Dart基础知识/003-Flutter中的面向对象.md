

# 【重要】带你揭开Flutter中的面向对象-辅导说明和源码

> main.dart

```dart
import 'package:flutter/material.dart';
import 'package:flutter_dart_learn/data_type.dart';
import 'package:flutter_dart_learn/oop_learn.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter必备Dart基础',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'Flutter必备Dart基础'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    _oopLearn();
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: ListView(
          children: <Widget>[
//            DataType(),
          ],
        ),
      ),
    );
  }

  void _oopLearn() {
    //创建Student的对象
    Student stu1 = Student('清华', 'Jack', 18);
    stu1.school = '985';
    print(stu1.toString());
    Student stu2 = Student('北大', 'Tom', 16, city: '上海', country: '中国');
    print(stu2.toString());

    Student.doPrint('_oopLearn');

    StudyFlutter sf = StudyFlutter();
    sf.study();

    Logger log1 = Logger();
    Logger log2 = Logger();
    print(log1 == log2);
  }
}


```

> oop_learn.dart

```dart
///面向对象（OOP）
class Student extends Person {
  //定义类的变量
  String _school; //通过下划线来标识私有字段（变量）
  String city;
  String country;
  String name;
  static Student instance;

  ///构造方法：
  ///通this.school初始化自有参数
  ///name,age交给父类进行初始化
  ///city为可选参数
  ///country设有默认参数
  Student(this._school, String name, int age,
      {this.city, this.country = 'China'})
      //初始化列表：除了调用父类构造器，在子类构造器方法体之前，你也可以初始化实例变量，不同的初始化变量之间用逗号分隔开
      : name = '$country.$city',
        //如果父类没有默认构造方法（无参构造方法），则需要在初始化列表中调用父类构造方法进行初始化
        super(name, age) {
    //构造方法体不是必须的
    print('构造方法体不是必须的');
  }

  //命名构造方法：[类名+.+方法名]
  //使用命名构造方法为类实现多个构造方法
  Student.cover(Student stu) : super(stu.name, stu.age) {
    print('命名构造方法');
  }

  //命名工厂构造方法：factory [类名+.+方法名]
  //它可以有返回值，而且不需要将类的final变量作为参数，是提供一种灵活获取类对象的方式。
  factory Student.stu(Student stu) {
    return Student(stu._school, stu.name, stu.age,
        city: stu.city, country: stu.country);
  }

  @override
  String toString() {
    return 'name:$name school:${this._school},city:$city,country:$country ${super.toString()}';
  }

  //可以为私有字段设置getter来让外界获取到私有字段
  String get school => _school;

  //可以为私有字段设置setter来控制外界对私有字段的修改
  set school(String value) {
    _school = value;
  }

  //静态方法
  static doPrint(String str) {
    print('doPrint:$str');
  }

  ///科普小知识：实例方法，对象的实例方法可以访问到实例变量与this，如上述代码中的toString
}

///定一个Dart类，所有类都继承自Object
class Person {
  String name;
  int age;

  Person(this.name, this.age);

  ///重写父类方法
  @override
  String toString() {
    return 'name:$name, age:$age';
  }
}

///工厂构造方法演示
class Logger {
  static Logger _cache;

//  工厂构造方法：
//  不仅仅是构造方法，更是一种模式
//  有时候为了返回一个之前已经创建的缓存对象，原始的构造方法已经不能满足要求
//  那么可以使用工厂模式来定义构造方法
  factory Logger() {
    if (_cache == null) {
      _cache = Logger._internal();
    }
    return _cache;
  }

  Logger._internal();

  void log(String msg) {
    print(msg);
  }
}

///继承抽象类要实现它的抽象方法，否则也需要将自己定义成抽象类
class StudyFlutter extends Study {
  @override
  void study() {
    print('Learning Flutter');
  }
}

///使用 abstract 修饰符来定义一个抽象类，该类不能被实例化。抽象类在定义接口的时候非常有用，实际上抽象中也包含一些实现
abstract class Study {
  void study();
}

///为类添加特征：mixins
///mixins 是在多个类层次结构中重用代码的一种方式
///要使用 mixins ，在 with 关键字后面跟一个或多个 mixin 的名字(用逗号分开)，并且with要用在extends关键字之后
///mixins的特征：实现 mixin ，就创建一个继承 Object 类的子类(不能继承其他类)，不声明任何构造方法，不调用 super
///猜猜上面的类中哪个是mixin？

class Test extends Person with Study {
  Test(String name, int age) : super(name, age);

  @override
  void study() {
    // TODO: implement study
  }
}

```