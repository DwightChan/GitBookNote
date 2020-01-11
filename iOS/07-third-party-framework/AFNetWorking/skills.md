# 使用技巧(Skills)

- 1.在开发的时候可以创建一个工具类，继承自我们的AFN中的请求管理者，再控制器中真正发请求的代码使用自己封装的工具类。
- 2.这样做的优点是以后如果修改了底层依赖的框架，那么我们修改这个工具类就可以了，而不用再一个一个的去修改。
- 3.该工具类一般提供一个单例方法，在该方法中会设置一个基本的请求路径。
- 4.该方法通常还会提供对GET或POST请求的封装。
- 5.在外面的时候通过该工具类来发送请求
- 6.单例方法：

  ```objc
  + (instancetype)shareNetworkTools
  {
      static XMGNetworkTools *instance;
      static dispatch_once_t onceToken;
      dispatch_once(&onceToken, ^{
          // 注意: BaseURL中一定要以/结尾
          instance = [[self alloc] initWithBaseURL:[NSURL URLWithString:@"http://120.25.226.186:32812/"]];
      });
      return instance;
  }
  ```

--- 
<br/>