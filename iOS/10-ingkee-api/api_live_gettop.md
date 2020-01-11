# api/live/gettop

获取视频

## URL

[http://service.ingkee.com/api/live/gettop ](http://service.ingkee.com/api/live/gettop )

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
| count     | true | string | 5                                        |
| multiaddr | true | string | 1                                        |





## 注意事项

无

## 返回结果

JSON示例

```objective-c
{
  "dm_error": 0,
  "error_msg": "操作成功",
  "lives": [
    {
      "city": "西安市",
      "creator": {
        "emotion": "单身",
        "inke_verify": 0,
        "verified": 0,
        "description": "什么时候才可以400W？",
        "gender": 0,
        "profession": "",
        "id": 4690917,
        "verified_reason": "",
        "nick": "磊哥哥",
        "location": "西安市",
        "birth": "1994-11-24",
        "hometown": "",
        "portrait": "OTc3MDkxNDY5Mjg1NDky.jpg",
        "gmutex": 1,
        "third_platform": "0",
        "level": 58,
        "rank_veri": 9,
        "veri_info": "白富美"
      },
      "id": "1469373798674353",
      "image": "",
      "name": "#再忙碌也需要直播##新人直播，求关注😂进来的宝宝点关注 谢谢💕#400！❤️",
      "pub_stat": 1,
      "room_id": 459961997,
      "share_addr": "http://live6.a8.com/s/?uid=4690917&liveid=1469373798674353&ctime=1469373798",
      "slot": 4,
      "status": 1,
      "stream_addr": "http://pull99.a8.com/live/1469373798674353.flv?ikHost=ws&ikOp=1&CodecInfo=8192",
      "version": 0,
      "online_users": 18362,
      "group": 1,
      "link": 0,
      "optimal": 0,
      "multi": 0
    },
    {
      "city": "",
      "creator": {
        "emotion": "保密",
        "inke_verify": 0,
        "verified": 0,
        "description": "情到深处自然刷",
        "gender": 1,
        "profession": "",
        "id": 6765363,
        "verified_reason": "",
        "nick": "明宇欧巴",
        "location": "",
        "birth": "1987-06-25",
        "hometown": "",
        "portrait": "NDM3OTUxNDY5MzU3MDAy.jpg",
        "gmutex": 0,
        "third_platform": "1",
        "level": 59,
        "rank_veri": 9,
        "veri_info": "高富帅"
      },
      "id": "1469373639182417",
      "image": "",
      "name": "天天向上",
      "pub_stat": 1,
      "room_id": 459954363,
      "share_addr": "http://live2.a8.com/s/?uid=6765363&liveid=1469373639182417&ctime=1469373639",
      "slot": 4,
      "status": 1,
      "stream_addr": "http://pull99.a8.com/live/1469373639182417.flv?ikHost=ws&ikOp=1&CodecInfo=8192",
      "version": 0,
      "online_users": 18570,
      "group": 1,
      "link": 0,
      "optimal": 0,
      "multi": 0
    },
    {
      "city": "天津市",
      "creator": {
        "emotion": "单身",
        "inke_verify": 1,
        "verified": 81,
        "description": "珍惜感恩。榜15+v",
        "gender": 0,
        "profession": "",
        "id": 3716098,
        "verified_reason": "企业法人",
        "nick": "井童小杏子",
        "location": "天津市",
        "birth": "1992-09-29",
        "hometown": "吉林省&长春市",
        "portrait": "OTE0MTExNDY3Nzk2MTcy.jpg",
        "gmutex": 0,
        "third_platform": "1",
        "level": 40,
        "rank_veri": 81,
        "veri_info": "企业法人"
      },
      "id": "1469373563436954",
      "image": "",
      "name": "",
      "pub_stat": 1,
      "room_id": 459950690,
      "share_addr": "http://live6.a8.com/s/?uid=3716098&liveid=1469373563436954&ctime=1469373563",
      "slot": 5,
      "status": 1,
      "stream_addr": "http://pull99.a8.com/live/1469373563436954.flv?ikHost=ws&ikOp=1&CodecInfo=8192",
      "version": 0,
      "online_users": 18732,
      "group": 1,
      "link": 0,
      "optimal": 0,
      "multi": 0
    },
    {
      "city": "厦门市",
      "creator": {
        "emotion": "保密",
        "inke_verify": 0,
        "verified": 0,
        "description": "💨",
        "gender": 0,
        "profession": "",
        "id": 8554382,
        "verified_reason": "",
        "nick": "一米的小短腿欧巴🙄",
        "location": "厦门市",
        "birth": "1997-09-18",
        "hometown": "福建省&厦门市",
        "portrait": "MTM1OTgxNDY4ODUyMzI0.jpg",
        "gmutex": 0,
        "third_platform": "0",
        "level": 33,
        "rank_veri": 6,
        "veri_info": "玉女"
      },
      "id": "1469373935981887",
      "image": "",
      "name": "#🎈直播随意🎀你聊我就聊🎈##新人直播，求关注😂进来的宝宝点关注 谢谢💕#",
      "pub_stat": 1,
      "room_id": 459968404,
      "share_addr": "http://live6.a8.com/s/?uid=8554382&liveid=1469373935981887&ctime=1469373935",
      "slot": 3,
      "status": 1,
      "stream_addr": "http://pull99.a8.com/live/1469373935981887.flv?ikHost=ws&ikOp=1&CodecInfo=8192",
      "version": 0,
      "online_users": 14345,
      "group": 1,
      "link": 0,
      "optimal": 0,
      "multi": 0
    },
    {
      "city": "北京市",
      "creator": {
        "emotion": "单身",
        "inke_verify": 1,
        "verified": 81,
        "description": "7.26凌晨00:00 我在这里等你们。不说不开心的 长了一岁 过去的过去吧",
        "gender": 1,
        "profession": "吹🐂逼",
        "id": 2425477,
        "verified_reason": "北京车影会汽车服务有限公司 董事长",
        "nick": "小峥、",
        "location": "北京市",
        "birth": "1987-07-25",
        "hometown": "北京市&",
        "portrait": "NTkyNzYxNDY5Mjg5Njcx.jpg",
        "gmutex": 1,
        "third_platform": "1",
        "level": 127,
        "rank_veri": 81,
        "veri_info": "北京车影会汽车服务有限公司 董事长"
      },
      "id": "1469373523921569",
      "image": "",
      "name": "",
      "pub_stat": 1,
      "room_id": 459948697,
      "share_addr": "http://live2.a8.com/s/?uid=2425477&liveid=1469373523921569&ctime=1469373523",
      "slot": 2,
      "status": 1,
      "stream_addr": "http://pull99.a8.com/live/1469373523921569.flv?ikHost=ws&ikOp=1&CodecInfo=8192",
      "version": 0,
      "online_users": 18348,
      "group": 1,
      "link": 0,
      "optimal": 0,
      "multi": 0
    }
  ],
  "expire_time": 5
}
```

代码示例:

http://service.ingkee.com/api/live/gettop?imsi=&uid=150633875&proto=7&idfa=E54DF3AE-FBD1-49B0-8F26-9973BEED9404&lc=0000000000000030&cc=TG0001&imei=&sid=20bUJGsWAjuqogNFHdEA9g0rBuz39eR8x9a18ti1RTWCaIhhZi2g&cv=IK3.2.60_Iphone&devi=9f574585642d2befc53f2e53ce7cc9adbd51c8da&conn=Wifi&ua=iPhone%205s&idfv=501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1&osversion=ios_9.200000&count=5&multiaddr=1


