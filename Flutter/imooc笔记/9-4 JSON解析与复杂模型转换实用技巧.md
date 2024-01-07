## JSON解析与复杂模型转换实用技巧

- 应该是有那种JSON序列化方式？
- 如何序列化？
- 复杂JSON解析？
- 提升效率：在线转换JSON TO Dart？

JSON是一种轻量级的数据交换语言，在网络编程中大量的用到了JSON来作为传输数据的格式，那么在Flutter中是如何处理JSON数据，以及JSON数据处理有那些实用技巧呢？

## 我该用什么JSON序列化方式？

- 小型项目：手动序列化；
- 大型项目：借助插件生成[json_serializable](https://pub.dartlang.org/packages/json_serializable)和[built_value](https://pub.dartlang.org/packages/built_value)；

> 其实大型项目使用手动+借助下面提到的[在线转换](http://www.devio.org/io/tools/json-to-dart/)的方式更加灵活高效；

## 如何反序列化？

```dart
String jsonStr = '{ "icon": "http://www.devio.org/io/flutter_app/img/ln_food.png", "title": "美食林", "url": "https://m.ctrip.com/webapp/you/foods/address.html?new=1&ishideheader=true", "statusBarColor": "19A0F0", "hideAppBar": true }';
Map<String, dynamic> map = JSON.decode(jsonStr);

print('icon： ${map['icon']}');
print('title：${map['title']}');
```

通过上述方式可以将json字符串转换成Map，但Map中存放那些字段在使用的时候很不方便，如果将`Map<String, dynamic>`转成Model呢？

```dart
...
CommonModel model = CommonModel.fromJson(map);
print('icon： ${model.icon}');
print('title：${model.title}');

...
class CommonModel {
  final String icon;
  final String title;
  final String url;
  final String statusBarColor;
  final bool hideAppBar;

  CommonModel({this.icon, this.title, this.url, this.statusBarColor, this.hideAppBar});

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

> 这样一来我们就可以很明确的指导model中有那些字段。

## 复杂JSON解析？

### 如何解析对象中的数组？

```
{
  "url": "xxx",
  "tabs": [
    {
      "labelName": "推荐",
      "groupChannelCode": "tourphoto_global1"
    },
    {
      "labelName": "拍照技巧",
      "groupChannelCode": "tab-photo"
    }
  ]
}
```

解析：

```dart
class TravelTabModel {
  String url;
  List<TravelTab> tabs;

  TravelTabModel({this.url, this.tabs});

  TravelTabModel.fromJson(Map<String, dynamic> json) {
	 url = json['url'];
    (json['tabs'] as List).map((i) => TravelTab.fromJson(i));
  }
}

class TravelTab {
  String labelName;
  String groupChannelCode;

  TravelTab({this.labelName, this.groupChannelCode});

  TravelTab.fromJson(Map<String, dynamic> json) {
    labelName = json['labelName'];
    groupChannelCode = json['groupChannelCode'];
  }
}
```

> 如果要加些异常处理：

```dart
TravelTabModel.fromJson(Map<String, dynamic> json) {
    url = json['url'];
    if (json['tabs'] != null) {
      tabs = new List<TravelTab>();
      json['tabs'].forEach((v) {
        tabs.add(new TravelTab.fromJson(v));
      });
    }
  }
```

> 改成final：

```
class TravelTabModel {
  final String url;
  final List<TravelTab> tabs;

  TravelTabModel({this.url, this.tabs});

  factory TravelTabModel.fromJson(Map<String, dynamic> json) {
    String url = json['url'];
    List<TravelTab> tabs =
        (json['tabs'] as List).map((i) => TravelTab.fromJson(i)).toList();
    return TravelTabModel(url: url, tabs: tabs);
  }
}
```

## 提升效率：在线转换JSON TO Dart？

- [home_page.json](http://www.devio.org/io/flutter_app/json/home_page.json)
- [`json_to_dart`](http://www.devio.org/io/tools/json-to-dart/)
- [json2dart](http://json2dart.com/)

