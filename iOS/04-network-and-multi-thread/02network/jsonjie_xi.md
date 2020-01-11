# JSON解析

<br/>

##0. 本节知识点:
1. JSON简单介绍
2. JSON解析
3. 字典转模型框架

--- 
<br/>
##1. JSON简单介绍
- **什么是JSON**
    - JSON是一种轻量级的数据格式，一般用于数据交互
    - 服务器返回给客户端的数据，一般都是JSON格式或者XML格式（文件下载除外）


- **相关说明**
    - JSON的格式很像OC中的字典和数组
    - **注意: **标准JSON格式key必须是双引号
        - 有些不标准的可能写成单引号, 安卓和 Java 可以解析
        - 但是苹果不能解析, 只能让后台改


- **JSON解析方案**
    - 第三方框架:
        - JSONKit
        - SBJSON
        - TouchJSON
    - 苹果原生（NSJSONSerialization）(性能最好)


--- 
<br/>
##2. JSON解析
- **1）json数据->OC对象**
    - 返序列化处理
    - NSJSONSerialization的常见方法


- **2）OC对象->JSON对象**
- **3）OC对象和JSON数据格式之间的一一对应关系**
- **4）如何查看复杂的JSON数据**
- **5）视频的简单播放**


- **NSJSONSerialization的常见方法**

  ```objc
  //JSON数据 -->> OC对象
  + (id)JSONObjectWithData:(NSData *)data options:(NSJSONReadingOptions)opt error:(NSError **)error;
  ```
  ```objc
  // OC对象 -->> JSON数据 
  + (NSData *)dataWithJSONObject:(id)obj options:(NSJSONWritingOptions)opt error:(NSError **)error;
  ```

- **相关代码**

  ```objc
  // 1）json数据->OC对象
  //把json数据转换为OC对象
  -(void)jsonToOC
  {
      //1. 确定url路径
      NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/login?username=33&pwd=33&type=JSON"];

      //2.创建一个请求对象
      NSURLRequest *request = [NSURLRequest requestWithURL:url];

      //3.使用NSURLSession发送一个异步请求
      [NSURLConnection sendAsynchronousRequest:request queue:[NSOperationQueue mainQueue] completionHandler:^(NSURLResponse * _Nullable response, NSData * _Nullable data, NSError * _Nullable connectionError) {

          //4.当接收到服务器响应的数据后，解析数据(JSON--->OC)

          /*
           第一个参数：要解析的JSON数据，是NSData类型也就是二进制数据
           第二个参数: 解析JSON的可选配置参数
           NSJSONReadingMutableContainers 解析出来的字典和数组是可变的
           NSJSONReadingMutableLeaves 解析出来的对象中的字符串是可变的  iOS7以后有问题
           NSJSONReadingAllowFragments 被解析的JSON数据如果既不是字典也不是数组, 那么就必须使用这个
           */
          NSDictionary *dict = [NSJSONSerialization JSONObjectWithData:data options:kNilOptions error:nil];
          NSLog(@"%@",dict);

      }];
  }
  ```
  ```objc
  // 2）OC对象->JSON对象
  //1.要转换成JSON数据的OC对象*这里是一个字典
  NSDictionary *dictM = @{
                          @"name":@"wendingding",
                          @"age":@100,
                          @"height":@1.72
                          };
  //2.OC->JSON
  /*
   注意：可以通过+ (BOOL)isValidJSONObject:(id)obj;方法判断当前OC对象能否转换为JSON数据
   具体限制：
       1.obj 是NSArray 或 NSDictionay 以及他们派生出来的子类
       2.obj 包含的所有对象是NSString,NSNumber,NSArray,NSDictionary 或NSNull
       3.字典中所有的key必须是NSString类型的
       4.NSNumber的对象不能是NaN或无穷大
   */
  /*
   第一个参数：要转换成JSON数据的OC对象，这里为一个字典
   第二个参数：NSJSONWritingPrettyPrinted对转换之后的JSON对象进行排版，无意义
   */
  NSData *data = [NSJSONSerialization dataWithJSONObject:dictM options:NSJSONWritingPrettyPrinted error:nil];

  //3.打印查看Data是否有值
  /*
   第一个参数：要转换为STring的二进制数据
   第二个参数：编码方式，通常采用NSUTF8StringEncoding
   */
  NSString *strM = [[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding];
  NSLog(@"%@",strM);
  ```
  ```objc
  //3）OC对象和JSON数据格式之间的一一对应关系
  -(void)oCWithJSON
  {
      //JSON的各种数据格式
      //NSString *test = @"\"wendingding\"";
      //NSString *test = @"true";
      NSString *test = @"{\"name\":\"wendingding\"}";

      //把JSON数据->OC对象,以便查看他们之间的一一对应关系
      //注意点：如何被解析的JSON数据如果既不是字典也不是数组（比如是NSString）, 那么就必须使用这NSJSONReadingAllowFragments
      id obj = [NSJSONSerialization JSONObjectWithData:[test dataUsingEncoding:NSUTF8StringEncoding] options:NSJSONReadingAllowFragments error:nil];

      NSLog(@"%@", [obj class]);

      /* JSON数据格式和OC对象的一一对应关系
           {} -> 字典
           [] -> 数组
           "" -> 字符串
           10/10.1 -> NSNumber
           true/false -> NSNumber
           null -> NSNull
       */
  }
  ```
  ```objc
  //4）如何查看复杂的JSON数据
  //方法一：
  //在线格式化http://tool.oschina.net/codeformat/json
  //方法二：
  //把解析后的数据写plist文件，通过plist文件可以直观的查看JSON的层次结构。
  [dictM writeToFile:@"/Users/chendehao/Desktop/videos.plist" atomically:YES];
  ```
  ```objc
  //5）视频的简单播放
  //0.需要导入系统框架
  #import <MediaPlayer/MediaPlayer.h>

  //1.拿到该cell对应的数据字典
  CDHVideo *video = self.videos[indexPath.row];

  // 拼接链接
  NSString *videoStr = [@"http://120.25.226.186:32812" stringByAppendingPathComponent:video.url];

  //2.创建一个视频播放器
  MPMoviePlayerViewController *vc = [[MPMoviePlayerViewController alloc]initWithContentURL:[NSURL URLWithString:videoStr]];

  //3.present播放控制器
  [self presentViewController:vc animated:YES completion:nil];
  ```
  ```objc
  - (void)writeJSON{

  //    /Users/chendehao/Desktop/课堂共享/新资料-多线程网络/0408多线程和网络-05/apps.plist
      NSArray *arrayM = [NSArray arrayWithContentsOfFile:@"/Users/chendehao/Desktop/课堂共享/新资料-多线程网络/0408多线程和网络-05/apps.plist"];
      // 无排版模式
  //    NSData *data = [NSJSONSerialization dataWithJSONObject:arrayM options:kNilOptions error:nil];
      // 有排版模式
      NSData *data = [NSJSONSerialization dataWithJSONObject:arrayM options:NSJSONWritingPrettyPrinted error:nil];
      NSLog(@"%@",[[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);
      // 写到桌面
      [data writeToFile:@"/Users/chendehao/Desktop/apps.json" atomically:YES];

  }
  ```
  ```objc
  - (void)readJSON{
      NSData *data = [NSData dataWithContentsOfFile:[[NSBundle mainBundle] pathForResource:@"apps.json" ofType:nil]];
      NSArray *array = [NSJSONSerialization JSONObjectWithData:data options:kNilOptions error:nil];
      NSLog(@"%@",array);
  }
  ```

--- 
<br/>

##3. 字典转模型框架
- **相关框架**
    - Mantle 需要继承自MTModel
    - JSONModel 需要继承自JSONModel
    - MJExtension 不需要继承，无代码侵入性

- **自己设计和选择框架时需要注意的问题**
    - 侵入性
    - 易用性，是否容易上手
    - 扩展性，很容易给这个框架增加新的功能

- **MJExtension框架的简单使用**

  ```objc
  //1.把字典数组转换为模型数组
      //使用MJExtension框架进行字典转模型
          self.videos = [CDHVideo mj_objectArrayWithKeyValuesArray:videoArray];

  //2.重命名模型属性的名称
  //第一种重命名属性名称的方法，有一定的代码侵入性
  //设置字典中的id被模型中的ID替换
  +(NSDictionary *)mj_replacedKeyFromPropertyName
  {
      return @{
               @"ID":@"id"
               };
  }

  //第二种重命名属性名称的方法，代码侵入性为零
  [CDHVideo mj_setupReplacedKeyFromPropertyName:^NSDictionary *{
      return @{
               @"ID":@"id"
               };
  }];
  //3.MJExtension框架内部实现原理-运行时
  ```

--- 
<br/>