


# 9-2 基于Http 实现网络操作

- import 'dart:convert'; 用于 请求 结果 respone 系列化；
```
    final result = json.decode(response.body);
  }
```

# 9-3 Future与 FutureBuilder 实用技巧

- Future 类似 js 中的 promise 使用

- FutureBuilder是一个将异步操作和异步UI更新结合在一起的类，通过它我们可以将网络请求，数据库读取等的结果更新的页面上。

- **注意**
```
  Utf8Decoder utf8decoder = Utf8Decoder(); //fix 中文乱码
    var result = json.decode(utf8decoder.convert(response.bodyBytes));
```

# 9-4 JSON解析与复杂模型转换实用技巧

- 小型项目：手动序列化；
- 大型项目：借助插件生成json_serializable和built_value；

- 借助第三方工具；

# 9-5 shared_preferences 数据存储