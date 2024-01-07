## 基于ListView实现水平和垂直方式滚动的列表

- 如何实现垂直滚动的列表？
- 如何实现水平滚动列表？

## 如何实现垂直滚动列表？

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());
const CITY_NAMES = [ '北京', '上海', '广州', '深圳', '杭州', '苏州', '成都', '武汉', '郑州', '洛阳', '厦门', '青岛', '拉萨' ];

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final title = 'Basic List';

    return MaterialApp(
      title: title,
      home: Scaffold(
        appBar: AppBar(
          title: Text(title),
        ),
        body: ListView(
          children: _buildList(),
        ),
      ),
    );
  }

  List<Widget> _buildList() {
    return CITY_NAMES.map((city) => _item(city)).toList();
  }

  Widget _item(String city) {
    return Container(
      height: 80,
      margin: EdgeInsets.only(bottom: 5),
      alignment: Alignment.center,
      decoration: BoxDecoration(color: Colors.teal),
      child: Text(
        city,
        style: TextStyle(color: Colors.white, fontSize: 20),
      ),
    );
  }
}
```

## 如何实现水平滚动列表？

```
import 'package:flutter/material.dart';

void main() => runApp(MyApp());
const CITY_NAMES = [ '北京', '上海', '广州', '深圳', '杭州', '苏州', '成都', '武汉', '郑州', '洛阳', '厦门', '青岛', '拉萨' ];

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final title = '水平';

    return MaterialApp(
      title: title,
      home: Scaffold(
        appBar: AppBar(
          title: Text(title),
        ),
        body: Container(
          height: 200,
          child: ListView(
            scrollDirection: Axis.horizontal,
            children: _buildList(),
          ),
        ),
      ),
    );
  }

  List<Widget> _buildList() {
    return CITY_NAMES.map((city) => _item(city)).toList();
  }

  Widget _item(String city) {
    return Container(
      width: 160,
      margin: EdgeInsets.only(right: 5),
      alignment: Alignment.center,
      decoration: BoxDecoration(color: Colors.teal),
      child: Text(
        city,
        style: TextStyle(color: Colors.white, fontSize: 20),
      ),
    );
  }
}
```

