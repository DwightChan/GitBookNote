# api/live/ticker

广告轮播器

## URL

[http://120.55.238.158/api/live/ticker](http://120.55.238.158/api/live/ticker  )

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
  "ticker": [
    {
      "image": "OTU5MDExNDY4ODE1MDc3.jpg",
      "link": "http://api.busi.inke.tv/html/service.html?web_entrance_id=1",
      "atom": 0
    },
    {
      "image": "NjU2NDIxNDYxOTQ2MTMy.jpg",
      "link": "http://live.a8.com/pages/renzheng.html?web_entrance_id=1",
      "atom": 0
    },
    {
      "image": "NzEyMTAxNDYxMzE2NDA3.jpg",
      "link": "http://meelive.cn/act/191.shtml",
      "atom": 0
    }
  ],
  "error_msg": "操作成功",
  "dm_error": 0
}
```

代码示例:

http://120.55.238.158/api/live/ticker?imsi=&uid=150633875&proto=7&idfa=E54DF3AE-FBD1-49B0-8F26-9973BEED9404&lc=0000000000000030&cc=TG0001&imei=&sid=20bUJGsWAjuqogNFHdEA9g0rBuz39eR8x9a18ti1RTWCaIhhZi2g&cv=IK3.2.60_Iphone&devi=9f574585642d2befc53f2e53ce7cc9adbd51c8da&conn=Wifi&ua=iPhone%205s&idfv=501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1&osversion=ios_9.200000



