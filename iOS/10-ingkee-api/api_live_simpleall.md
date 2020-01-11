# api/live/simpleall

缩略视图(200个)

## URL

[http://120.55.238.158/api/live/simpleall](http://120.55.238.158/api/live/simpleall  )

## 支持格式

JSON

## HTTP请求方式

GET

## 是否需要登录

是

## 访问授权限制

访问级别：普通接口
频次限制：否

## 请求参数

|           | 必选   | 类型及范围  | 说明                                       |
| --------- | ---- | ------ | ---------------------------------------- |
| uid       | true | string | 用户ID 150633875                           |
| imsi      | true | string | 空值                                       |
| proto     | true | string | 7                                        |
| idfa      | true | string | E54DF3AE-FBD1-49B0-8F26-9973BEED9404     |
| lc        | true | string | 0000000000000030                         |
| cc        | true | string | TG0001                                   |
| imei      | true | string | 空值                                       |
| sid       | true | string | 20bUJGsWAjuqogNFHdEA9g0rBuz39eR8x9a18ti1RTWCaIhhZi2g |
| cv        | true | string | IK3.2.60_Iphone                          |
| devi      | true | string | 9f574585642d2befc53f2e53ce7cc9adbd51c8da |
| conn      | true | string | Wifi                                     |
| ua        | true | string | iPhone%205s                              |
| idfv      | true | string | 501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1     |
| osversion | true | string | ios_9.200000                             |
|           |      |        |                                          |



## 返回结果

JSON示例

```objective-c
{
  "dm_error": 0,
  "error_msg": "操作成功",
  "lives": [
    {
      "creator": {
        "id": 4732044,
        "level": 53,
        "nick": "双胞胎姐妹【大m小m】",
        "portrait": "MTM4NDUxNDYzMDI4NTMz.jpg"
      },
      "id": "1469413680610202",
      "name": "",
      "city": "黑河市",
      "share_addr": "http://live2.a8.com/s/?uid=4732044&liveid=1469413680610202&ctime=1469413680",
      "stream_addr": "http://pull99.a8.com/live/1469413680610202.flv?ikHost=ws&ikOp=1&CodecInfo=8192",
      "version": 0,
      "slot": 1,
      "optimal": 0,
      "online_users": 19780,
      "group": 0,
      "link": 0,
      "multi": 0,
      "rotate": 0
    },
    {
      "creator": {
        "id": 2096283,
        "level": 22,
        "nick": "👑甜心（没有推送请重新关注）",
        "portrait": "NDk0NTExNDY3NjQ3NjA3.jpg"
      },
      "id": "1469413964479972",
      "name": "#再忙碌也需要直播#",
      "city": "北京市",
      "share_addr": "http://live4.a8.com/s/?uid=2096283&liveid=1469413964479972&ctime=1469413964",
      "stream_addr": "http://pull99.a8.com/live/1469413964479972.flv?ikHost=ws&ikOp=1&CodecInfo=8192",
      "version": 0,
      "slot": 4,
      "optimal": 0,
      "online_users": 16117,
      "group": 0,
      "link": 0,
      "multi": 0,
      "rotate": 0
    },
    ...(以下198个省略)
  "expire_time": 60
}
```



示例

http://120.55.238.158/api/live/simpleall?imsi=&uid=150633875&proto=7&idfa=E54DF3AE-FBD1-49B0-8F26-9973BEED9404&lc=0000000000000030&cc=TG0001&imei=&sid=20bUJGsWAjuqogNFHdEA9g0rBuz39eR8x9a18ti1RTWCaIhhZi2g&cv=IK3.2.60_Iphone&devi=9f574585642d2befc53f2e53ce7cc9adbd51c8da&conn=Wifi&ua=iPhone%205s&idfv=501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1&osversion=ios_9.200000&

请求方法:

```objective-c
- (void)sendRequest:(id)sender
{
   
    NSURLSessionConfiguration* sessionConfig = [NSURLSessionConfiguration defaultSessionConfiguration];
 
    /* Create session, and optionally set a NSURLSessionDelegate. */
    NSURLSession* session = [NSURLSession sessionWithConfiguration:sessionConfig delegate:nil delegateQueue:nil];

    /* Create the Request:
       My API (GET http://120.55.238.158/api/live/simpleall)
     */

    NSURL* URL = [NSURL URLWithString:@"http://120.55.238.158/api/live/simpleall"];
    NSDictionary* URLParams = @{
        @"imsi": @"",
        @"uid": @"150633875",
        @"proto": @"7",
        @"idfa": @"E54DF3AE-FBD1-49B0-8F26-9973BEED9404",
        @"lc": @"0000000000000030",
        @"cc": @"TG0001",
        @"imei": @"",
        @"sid": @"20bUJGsWAjuqogNFHdEA9g0rBuz39eR8x9a18ti1RTWCaIhhZi2g",
        @"cv": @"IK3.2.60_Iphone",
        @"devi": @"9f574585642d2befc53f2e53ce7cc9adbd51c8da",
        @"conn": @"Wifi",
        @"ua": @"iPhone 5s",
        @"idfv": @"501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1",
        @"osversion": @"ios_9.200000",
    };
    URL = NSURLByAppendingQueryParameters(URL, URLParams);
    NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:URL];
    request.HTTPMethod = @"GET";

    // Headers

    [request addValue:@"aliyungf_tc=AQAAAEYrBy9KiwcAxDvFeJzzvJN0bZZV" forHTTPHeaderField:@"Cookie"];

    /* Start a new Task */
    NSURLSessionDataTask* task = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
        if (error == nil) {
            // Success
            NSLog(@"URL Session Task Succeeded: HTTP %ld", ((NSHTTPURLResponse*)response).statusCode);
        }
        else {
            // Failure
            NSLog(@"URL Session Task Failed: %@", [error localizedDescription]);
        }
    }];
    [task resume];
}

/*
 * Utils: Add this section before your class implementation
 */

/**
 This creates a new query parameters string from the given NSDictionary. For
 example, if the input is @{@"day":@"Tuesday", @"month":@"January"}, the output
 string will be @"day=Tuesday&month=January".
 @param queryParameters The input dictionary.
 @return The created parameters string.
*/
static NSString* NSStringFromQueryParameters(NSDictionary* queryParameters)
{
    NSMutableArray* parts = [NSMutableArray array];
    [queryParameters enumerateKeysAndObjectsUsingBlock:^(id key, id value, BOOL *stop) {
        NSString *part = [NSString stringWithFormat: @"%@=%@",
            [key stringByAddingPercentEscapesUsingEncoding: NSUTF8StringEncoding],
            [value stringByAddingPercentEscapesUsingEncoding: NSUTF8StringEncoding]
        ];
        [parts addObject:part];
    }];
    return [parts componentsJoinedByString: @"&"];
}

/**
 Creates a new URL by adding the given query parameters.
 @param URL The input URL.
 @param queryParameters The query parameter dictionary to add.
 @return A new NSURL.
*/
static NSURL* NSURLByAppendingQueryParameters(NSURL* URL, NSDictionary* queryParameters)
{
    NSString* URLString = [NSString stringWithFormat:@"%@?%@",
        [URL absoluteString],
        NSStringFromQueryParameters(queryParameters)
    ];
    return [NSURL URLWithString:URLString];
}

```



