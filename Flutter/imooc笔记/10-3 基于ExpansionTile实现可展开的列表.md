## 基于ExpansionTile实现可展开的列表

## 认识ExpansionTile

```dart
const ExpansionTile({
    Key key,
    this.leading,//标题左侧要展示的widget
    @required this.title,//要展示的标题widget
    this.backgroundColor,//背景
    this.onExpansionChanged,//列表展开收起的回调函数
    this.children = const <Widget>[],//列表展开时显示的widget
    this.trailing,//标题有侧要展示的widget
    this.initiallyExpanded = false,//是否默认状态下展开
  })
```

## 如何实现可折叠的列表？

- 数据要求
- `ExpansionTile`

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());
const CITY_NAMES = {
  '北京': ['东城区', '西城区', '朝阳区', '丰台区', '石景山区', '海淀区', '顺义区'],
  '上海': ['黄浦区', '徐汇区', '长宁区', '静安区', '普陀区', '闸北区', '虹口区'],
  '广州': ['越秀', '海珠', '荔湾', '天河', '白云', '黄埔', '南沙', '番禺'],
  '深圳': ['南山', '福田', '罗湖', '盐田', '龙岗', '宝安', '龙华'],
  '杭州': ['上城区', '下城区', '江干区', '拱墅区', '西湖区', '滨江区'],
  '苏州': ['姑苏区', '吴中区', '相城区', '高新区', '虎丘区', '工业园区', '吴江区']
};

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final title = '列表展开与收起';

    return MaterialApp(
      title: title,
      home: Scaffold(
        appBar: AppBar(
          title: Text(title),
        ),
        body: Container(
          child: ListView(
            children: _buildList(),
          ),
        ),
      ),
    );
  }

  List<Widget> _buildList() {
    List<Widget> widgets = [];
    CITY_NAMES.keys.forEach((key) {
      widgets.add(_item(key, CITY_NAMES[key]));
    });
    return widgets;
  }

  Widget _item(String city, List<String> subCities) {
    return ExpansionTile(
      title: Text(
        city,
        style: TextStyle(color: Colors.black54, fontSize: 20),
      ),
      children: subCities.map((subCity) => _buildSub(subCity)).toList(),
    );
  }

  Widget _buildSub(String subCity) {
    return FractionallySizedBox(
        widthFactor: 1,
        child: Container(
          height: 50,
          margin: EdgeInsets.only(bottom: 5),
          decoration: BoxDecoration(color: Colors.lightBlueAccent),
          child: Text(subCity),
        ));
  }
}
```

> 