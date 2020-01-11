# 中文转码问题

<br/>

- URL是不支持中文, 因此如果URL字符串中包含中文那么在发送请求之前需要对URL进行中文转码
- 注意浏览器中的 `http` 的链接有时候可以看到有中文, 其实URL内部已经做了转码处理
- 如何对URL进行转码：`stringByAddingPercentEscapesUsingEncoding`
- **建议:**不管有没有中文字符, 都写上转码, 这样扩展性比较好


---

```ObjectiveC
-(void)get
{
    //http://120.25.226.186:32812/login2?username=%E5%B0%8F%E7%A0%81%E5%93%A5&pwd=520it&type=JSON
    // NSString *urlStr = @"http://120.25.226.186:32812/login2?username=%E5%B0%8F%E7%A0%81%E5%93%A5&pwd=520it&type=JSON";

    // 建议在开发中都多写一步转码操作

    // url 是不支持中文, 因此当字符串中包含中文的时候需要转码
    // 有时候在浏览器的 url 上能看到有中文情况是因为浏览器做了处理, 发送的是转码后的的内容
    NSString *urlStr = @"http://120.25.226.186:32812/login2?username=小码哥&pwd=520it&type=JSON";

    // 打印转码前
    NSLog(@"start++++%@",urlStr);
    urlStr = [urlStr stringByAddingPercentEscapesUsingEncoding:NSUTF8StringEncoding];
    // 打印转码后
    NSLog(@"end++++%@",urlStr);

    //1.url
    NSURL *url = [NSURL URLWithString:urlStr];

    //2.创建请求对象
    NSURLRequest *request = [NSURLRequest requestWithURL:url];

    //3.发送请求
    [NSURLConnection sendAsynchronousRequest:request queue:[NSOperationQueue mainQueue] completionHandler:^(NSURLResponse * _Nullable response, NSData * _Nullable data, NSError * _Nullable connectionError) {

        if (connectionError) {
            NSLog(@"%@--",connectionError);
            return ;
        }
        //4.解析数据
        NSLog(@"%@",[[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding]);
    }];
}
```

---
```ObjectiveC
-(void)post
{
    //0.urlstr
    NSString *urlStr = @"http://120.25.226.186:32812/login2";

    //1.url
    NSURL *url = [NSURL URLWithString:urlStr];

    //2.创建请求对象
    NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];

    //2.1 修改请求方法为POST
    request.HTTPMethod = @"POST";

    //2.2 设置请求体
    request.HTTPBody = [@"username=小码哥&pwd=520it&type=JSON" dataUsingEncoding:NSUTF8StringEncoding];

    //3.发送请求
    [NSURLConnection sendAsynchronousRequest:request queue:[NSOperationQueue mainQueue] completionHandler:^(NSURLResponse * _Nullable response, NSData * _Nullable data, NSError * _Nullable connectionError) {

        if (connectionError) {
            NSLog(@"%@--",connectionError);
            return ;
        }
        //4.解析数据
        NSLog(@"%@",[[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding]);
    }];
}
```

  
---
<br/>
