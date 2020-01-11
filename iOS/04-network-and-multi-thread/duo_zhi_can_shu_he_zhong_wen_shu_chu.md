# 多值参数和中文输出

<br/>


##1. 多值参数
- **如果一个参数对应着多个值，那么直接按照"参数=值&参数=值"的方式拼接**

  ```objc
  /*
   如果一个参数对应着多个值，那么直接按照"参数=值&参数=值"的方式拼接
   */
  - (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{
      //1.url
      //http://120.25.226.186:32812/weather?place=Beijing

      //错误的写法:  http://120.25.226.186:32812/weather?place=Beijing&guangzhou
      //           错误写法的后面的参数会被忽略
      //正确的写法:  http://120.25.226.186:32812/weather?place=Beijing&place=guangzhou

      NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/weather?place=Beijing&place=guangzhou"];

      //2. 发送请求
      [[[NSURLSession sharedSession] dataTaskWithURL:url completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {
          NSLog(@"%@",[[NSString alloc] initWithData:data  encoding:NSUTF8StringEncoding]);

          // 3. json 数据解析
          NSDictionary *dict = [NSJSONSerialization JSONObjectWithData:data options:kNilOptions error:nil];
          NSLog(@"%@",dict);
          // 注意: 一定要启动任务
      }] resume];

      NSDictionary *obj = @{@"name": @"dashenban"};
      NSLog(@"%@",obj);
  }
  ```
    
---
<br/>

##2. 如何解决字典和数组中输出乱码的问题 
- **给字典和数组添加一个分类，重写descriptionWithLocale方法，在该方法中拼接元素格式化输出。**

  ```objc
  -(nonnull NSString *)descriptionWithLocale:(nullable id)locale
  ```
  
- **给字典一个分类，重写descriptionWithLocale方法，在该方法中拼接元素格式化输出。**
  
  ```objc
  #import <Foundation/Foundation.h>
  @implementation NSDictionary (Log)

  - (NSString *)descriptionWithLocale:(id)locale indent:(NSUInteger)level{

      NSMutableString *string = [NSMutableString string];

      //该方法控制字典的输出内容, 如果重写了这个方法, 整个项目中所有字典的打印输出都是这样输出
      //return @"我是一个字典";

      //拼接字符串,控制器输出的格式和内容
      [string appendString:@"{\n"];

      [self enumerateKeysAndObjectsUsingBlock:^(id  _Nonnull key, id  _Nonnull obj, BOOL * _Nonnull stop) {
          [string appendFormat:@"%@",key];
          [string appendFormat:@"%@",obj];
      }];

      [string appendString:@"}"];

      // 删除最后一个逗号
      NSRange range = [string rangeOfString:@"," options:NSBackwardsSearch];
      if (range.location != NSNotFound) {
          [string deleteCharactersInRange:range];
      }
      return string;
  }
  @end
  ```
  
- **给数组添加一个分类，重写descriptionWithLocale方法，在该方法中拼接元素格式化输出。**
  
  ```objc
  #import <Foundation/Foundation.h>

  @implementation NSArray (Log)

  - (NSString *)descriptionWithLocale:(id)locale indent:(NSUInteger)level{

      NSMutableString *string = [NSMutableString string];

      //该方法控制字典的输出内容, 如果重写了这个方法, 整个项目中所有字典的打印输出都是这样输出
      //return @"我是一个字典";

      //拼接字符串,控制器输出的格式和内容
      [string appendString:@"[\n"];

      [self enumerateObjectsUsingBlock:^(id  _Nonnull obj, NSUInteger idx, BOOL * _Nonnull stop) {
          [string appendFormat:@"%@",obj];
      }];

      [string appendString:@"]"];

      // 删除最后一个逗号
      NSRange range = [string rangeOfString:@"," options:NSBackwardsSearch];
      if (range.location != NSNotFound) {
          [string deleteCharactersInRange:range];
      }
      return string;
  }

  @end
  ```

---
<br/>