# 序列化处理(Serialize)

- **1.AFN它内部默认把服务器响应的数据当做json来进行解析，所以如果服务器返回给我的不是JSON数据那么请求报错，这个时候需要设置AFN对响应信息的解析方式。AFN提供了三种解析响应信息的方式，分别是：**
    - AFXMLParserResponseSerializer----XML
    - AFHTTPResponseSerializer----------默认二进制响应数据
    - AFJSONResponseSerializer----------JSON


- **2.还有一种情况就是服务器返回给我们的数据格式不太一致（开发者工具Content-Type:text/xml）,那么这种情况也有可能请求不成功。解决方法:**
    - 直接在源代码中修改，添加相应的Content-Type
    - 拿到这个属性，添加到它的集合中


- **相关代码**

  ```objc
  -(void)srializer
  {
      //1.创建请求管理者，内部基于NSURLSession
      AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];

      /* 知识点1：设置AFN采用什么样的方式来解析服务器返回的数据*/

      //如果返回的是XML，那么告诉AFN，响应的时候使用XML的方式解析 
      // 注意: 解析 xml 格式时, 要创建解析器, 给解析通过解析对象的代理方法来解析数据, 
      manager.responseSerializer = [AFXMLParserResponseSerializer serializer];

      //如果返回的就是二进制数据，那么采用默认二进制的方式来解析数据
      //manager.responseSerializer = [AFHTTPResponseSerializer serializer];

      //采用JSON的方式来解析数据 , 默认是 JSON 方式 ,因此可以不写
      //manager.responseSerializer = [AFJSONResponseSerializer serializer];

      /*知识点2 告诉AFN，再序列化服务器返回的数据的时候，支持此种类型*/
      [AFJSONResponseSerializer serializer].acceptableContentTypes = [NSSet setWithObject:@"text/xml"];

      //2.把所有的请求参数通过字典的方式来装载，GET方法内部会自动把所有的键值对取出以&符号拼接并最后用？符号连接在请求路径后面
      NSDictionary *dict = @{
                             @"username":@"223",
                             @"pwd":@"ewr",
                             @"type":@"XML"
                             };

      //3.发送GET请求
      [manager GET:@"http://120.25.226.186:32812/login" parameters:dict success:^(NSURLSessionDataTask * _Nonnull task, id  _Nonnull responseObject) {

          //4.请求成功的回调block
          NSLog(@"%@",[responseObject class]);
      } failure:^(NSURLSessionDataTask * _Nonnull task, NSError * _Nonnull error) {

          //5.请求失败的回调，可以打印error的值查看错误信息
          NSLog(@"%@",error);
      }];
  }
  ```
  ```objc
  #pragma  mark - Methods
  - (void)json{

      // 1. 创建一个会话管理者
      AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];

      /*
       1)afn内部默认已经完成了JSON解析工作
       优点:方便
       缺点:如果服务器返回的数据不是JSON会报错
       */
       NSDictionary *dict = @{@"type":@"JSON"};
      // 2. 发送请求
      [manager GET:@"http://120.25.226.186:32812/video" parameters:dict progress:nil success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
          NSLog(@"%@---%@",[responseObject class],responseObject);
      } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
          NSLog(@"%@----",error);
      }];
  }
  ```
  ```objc
  -(void)xml{
      // 1. 创建一个会话管理者
      AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];
      // afn内部默认已经完成了JSON解析工作 所以我们必须修改为 xml 来解析数据
      // 注意: 这里一定要设置为 xml 的方式来解析数据
      manager.responseSerializer = [AFXMLParserResponseSerializer serializer];
      NSDictionary *dict = @{@"type":@"XML"};
      // 2. 发送请求
      [manager GET:@"http://120.25.226.186:32812/video" parameters:dict progress:nil success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {

          // 1. 创建解析器
          NSXMLParser *parser = (NSXMLParser *)responseObject;

          // 2. 设置代理
          parser.delegate = self;

          // 3. 开始解析
          [parser parse];

          NSLog(@"%@---%@",[responseObject class],responseObject);
      } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
          NSLog(@"%@----",error);
      }];
  }

  #pragma mark - NSXMLParserDelegate
  - (void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName attributes:(NSDictionary<NSString *,NSString *> *)attributeDict{
      // 这里只是简单将每个元素打印出来, 没有添加到数组中
      NSLog(@"%@----%@", elementName,attributeDict);
  }
  ```
  ```objc
  // 服务器返回的既不是json 也不是 xml , 而是二进制数据的时候就不做处理
  - (void)httpData{
      // 1. 穿件会话管理者
      AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];

      // 设置不做处理
      manager.responseSerializer = [AFHTTPResponseSerializer serializer];

      // 2. 发送请求
      [manager GET:@"http://120.25.226.186:32812/resources/images/minion_02.png" parameters:nil progress:nil success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {

          NSLog(@"%@---%@",[responseObject class],responseObject);
          NSLog(@"%@",task);

      } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
          NSLog(@"%@---------",error);
      }];
  }
  ```

---
<br />