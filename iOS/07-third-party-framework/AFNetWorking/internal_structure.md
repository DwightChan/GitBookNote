# 内部结构(Internal structure)

- **NSURLConnection**
    + AFURLConnectionOperation(已经被废弃)
    + AFHTTPRequestOperation(已经被废弃)
    + AFHTTPRequestOperationManager(封装了常用的 HTTP 方法)(已经被废弃)
        * 属性
            * baseURL :AFN建议开发者针对 AFHTTPRequestOperationManager 自定义个一个单例子类，设置 baseURL, 所有的网络访问，都只使用相对路径即可
            * requestSerializer :请求数据格式/默认是二进制的 HTTP
            * responseSerializer :响应的数据格式/默认是 JSON 格式
            * operationQueue
            * reachabilityManager :网络连接管理器
        * 方法
            * manager :方便创建管理器的类方法
            * HTTPRequestOperationWithRequest :在访问服务器时，如果要告诉服务器一些附加信息，都需要在 Request 中设置
            * GET
            * POST


- **NSURLSession**
    + AFURLSessionManager
    + AFHTTPSessionManager(封装了常用的 HTTP 方法)
        * GET
        * POST
        * UIKit + AFNetworking 分类
        * NSProgress :利用KVO


- **半自动的序列化&反序列化的功能**
    + AFURLRequestSerialization :请求的数据格式/默认是二进制的
    + AFURLResponseSerialization :响应的数据格式/默认是JSON格式


- **附加功能**
    + 安全策略
        * HTTPS
        * AFSecurityPolicy
    + 网络检测
        * 对苹果的网络连接检测做了一个封装
        * AFNetworkReachabilityManager


- **建议:** 可以学习下AFN对 UIKit 做了一些分类, 对自己能力提升是非常有帮助的


--- 
<br/>

