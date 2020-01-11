# api/live/users

用户信息

## URL

[http://120.55.238.158/api/live/users](http://120.55.238.158/api/live/users )

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
| count     | true | string | 20                                       |
| id        | true | string | 1469357828536338                         |
| start     | true | string | 0                                        |



## 返回结果

JSON示例

```objective-c
{
  "dm_error": 0,
  "error_msg": "操作成功",
  "total": 351,
  "users": [
    {
      "emotion": "",
      "inke_verify": 0,
      "verified": 0,
      "description": "",
      "gender": 0,
      "profession": "",
      "id": 9723897,
      "verified_reason": "",
      "nick": "好想有个你",
      "location": "天津市",
      "birth": "",
      "hometown": "",
      "portrait": "http://wx.qlogo.cn/mmopen/gRvUTBLYaicibIkgQwORsXEXwiaUxw1RfibhGpLRF3FyiaqxYBWxflAD00qjWqXtt8QDHwjg4KxXdnfibBBu05fn1ic5gd55kNJ87l2/0",
      "gmutex": 0,
      "third_platform": "1",
      "level": 4,
      "rank_veri": 3,
      "veri_info": ""
    },
    {
      "emotion": "",
      "inke_verify": 0,
      "verified": 0,
      "description": "WX号feifei28274598",
      "gender": 0,
      "profession": "",
      "id": 35964517,
      "verified_reason": "",
      "nick": "💋 艾菲儿💋",
      "location": "西安市",
      "birth": "",
      "hometown": "",
      "portrait": "MTIyNjUxNDY5MTA2MDMx.jpg",
      "gmutex": 0,
      "third_platform": "1",
      "level": 4,
      "rank_veri": 3,
      "veri_info": ""
    },
    {
      "emotion": "",
      "inke_verify": 0,
      "verified": 0,
      "description": "",
      "gender": 1,
      "profession": "",
      "id": 3946176,
      "verified_reason": "",
      "nick": "☀我脚心痒痒",
      "location": "天津市",
      "birth": "",
      "hometown": "",
      "portrait": "NDc2NTYxNDY4NTc3Mzk0.jpg",
      "gmutex": 0,
      "third_platform": "1",
      "level": 12,
      "rank_veri": 3,
      "veri_info": ""
    },
    {
      "emotion": "",
      "inke_verify": 0,
      "verified": 0,
      "description": "",
      "gender": 0,
      "profession": "",
      "id": 147241943,
      "verified_reason": "",
      "nick": "笑的撕心裂肺",
      "location": "镇江市",
      "birth": "",
      "hometown": "",
      "portrait": "http://q.qlogo.cn/qqapp/1104658198/ED371F32D9CB09C9E421252EE1770AAB/100",
      "gmutex": 0,
      "third_platform": "0",
      "level": 3,
      "rank_veri": 3,
      "veri_info": ""
    },
    {
      "emotion": "",
      "inke_verify": 0,
      "verified": 0,
      "description": "",
      "gender": 1,
      "profession": "",
      "id": 57863454,
      "verified_reason": "",
      "nick": "东北小平",
      "location": "天津市",
      "birth": "",
      "hometown": "",
      "portrait": "http://wx.qlogo.cn/mmopen/Q3auHgzwzM6eJAkTsykFfsBGIZhNbPrVt9mq1HROOsBF0oe77GrLMl0PeLaDK7vhHOneGJns4k7oaqjSkAVDEg/0",
      "gmutex": 0,
      "third_platform": "0",
      "level": 17,
      "rank_veri": 4,
      "veri_info": "正太"
    },
    {
      "emotion": "",
      "inke_verify": 0,
      "verified": 0,
      "description": "",
      "gender": 1,
      "profession": "",
      "id": 40690456,
      "verified_reason": "",
      "nick": "平烦人生💕比烦人还烦",
      "location": "上海市",
      "birth": "",
      "hometown": "",
      "portrait": "http://wx.qlogo.cn/mmopen/Pf0P8KjjOib8ibK763c4VWiaIgvStfPNicowv7Aa6jjL6vhwyJFQeo7xnia4PY91vHM0dxucFibjWCNHIUOPn0bPibJ4Kib0ibWYpjo1U/0",
      "gmutex": 0,
      "third_platform": "1",
      "level": 3,
      "rank_veri": 3,
      "veri_info": ""
    },
    {
      "emotion": "",
      "inke_verify": 0,
      "verified": 0,
      "description": "",
      "gender": 1,
      "profession": "",
      "id": 99969112,
      "verified_reason": "",
      "nick": "大家好",
      "location": "长沙市",
      "birth": "",
      "hometown": "",
      "portrait": "http://wx.qlogo.cn/mmopen/WmwqjsSBsZIUGTGMd0gy67n81rskmPKjMATxHEHcFqUWLeQicqKQzzXViaX1hkdEmYQJPaEGVtlWb5cz1V6DW8fNcZDJqO41iaT/0",
      "gmutex": 0,
      "third_platform": "0",
      "level": 4,
      "rank_veri": 3,
      "veri_info": ""
    },
    {
      "emotion": "",
      "inke_verify": 0,
      "verified": 0,
      "description": "",
      "gender": 1,
      "profession": "",
      "id": 5745648,
      "verified_reason": "",
      "nick": "将心比心",
      "location": "天津市",
      "birth": "",
      "hometown": "",
      "portrait": "OTgwNTUxNDYzMjIzOTAy.jpg",
      "gmutex": 0,
      "third_platform": "1",
      "level": 5,
      "rank_veri": 3,
      "veri_info": ""
    },
    {
      "emotion": "",
      "inke_verify": 0,
      "verified": 0,
      "description": "",
      "gender": 1,
      "profession": "",
      "id": 67354836,
      "verified_reason": "",
      "nick": "Zpppppp💋",
      "location": "济宁市",
      "birth": "",
      "hometown": "",
      "portrait": "NzIzMjIxNDY4Mzk0NzAz.jpg",
      "gmutex": 0,
      "third_platform": "0",
      "level": 6,
      "rank_veri": 3,
      "veri_info": ""
    },
    {
      "emotion": "",
      "inke_verify": 0,
      "verified": 0,
      "description": "",
      "gender": 0,
      "profession": "",
      "id": 122426493,
      "verified_reason": "",
      "nick": "💓雯宝贝💓",
      "location": "",
      "birth": "",
      "hometown": "浙江省&台州市",
      "portrait": "MTkyMzYxNDY4NzU5Mzkz.jpg",
      "gmutex": 0,
      "third_platform": "0",
      "level": 6,
      "rank_veri": 3,
      "veri_info": ""
    }
  ]
}
```

示例


http://120.55.238.158/api/live/users?imsi=&uid=150633875&proto=7&idfa=E54DF3AE-FBD1-49B0-8F26-9973BEED9404&lc=0000000000000030&cc=TG0001&imei=&sid=20bUJGsWAjuqogNFHdEA9g0rBuz39eR8x9a18ti1RTWCaIhhZi2g&cv=IK3.2.60_Iphone&devi=9f574585642d2befc53f2e53ce7cc9adbd51c8da&conn=Wifi&ua=iPhone%205s&idfv=501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1&osversion=ios_9.200000&count=20&id=1469357828536338&start=0


