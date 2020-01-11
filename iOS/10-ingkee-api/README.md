# My Awesome Book

# 映客API

# api/live

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

# api/info

获取信息

## URL

[http://120.55.238.158/api/live/infos ](http://120.55.238.158/api/live/infos  )

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
| id        | true | string | 1469357062262570%2C1469356863401977%2C1469356844968217%2C1469356943418419%2C1469357103083633 |
| multiaddr | true | string | 1                                        |







## 返回结果

JSON示例

```objective-c
{
  "dm_error": 0,
  "error_msg": "操作成功",
  "lives": [
    {
      "city": "合肥市",
      "creator": {
        "emotion": "单身",
        "inke_verify": 0,
        "verified": 0,
        "description": "宝宝们，24号25号两天有事不直播",
        "gender": 1,
        "profession": "",
        "id": 690786,
        "verified_reason": "",
        "nick": "Dylan",
        "location": "合肥市",
        "birth": "2015-11-17",
        "hometown": "",
        "portrait": "MjcwNDkxNDY4NDIyNDk0.jpg",
        "gmutex": 1,
        "third_platform": "1",
        "level": 27,
        "rank_veri": 5,
        "veri_info": "怪蜀黍"
      },
      "id": "1469357062262570",
      "image": "",
      "name": "",
      "pub_stat": 1,
      "room_id": 458939437,
      "share_addr": "http://live7.a8.com/s/?uid=690786&liveid=1469357062262570&ctime=1469357062",
      "slot": 1,
      "status": 0,
      "stream_addr": "http://pull99.a8.com/live/1469357062262570.flv?ikHost=ws&ikOp=1&CodecInfo=8192",
      "version": 0,
      "online_users": 18091,
      "group": 0,
      "link": 0,
      "optimal": 0,
      "multi": 0,
      "rotate": 0
    },
    {
      "city": "武汉市",
      "creator": {
        "emotion": "保密",
        "inke_verify": 0,
        "verified": 0,
        "description": "微了个信：Shuangziman522\n微了个博：我是雙子Man",
        "gender": 1,
        "profession": "",
        "id": 2538608,
        "verified_reason": "",
        "nick": "雙子Man",
        "location": "武汉市",
        "birth": "2015-05-21",
        "hometown": "火星&",
        "portrait": "NjUyNTcxNDY4NzgzMTQ0.jpg",
        "gmutex": 1,
        "third_platform": "1",
        "level": 96,
        "rank_veri": 13,
        "veri_info": "霸道总裁"
      },
      "id": "1469356863401977",
      "image": "",
      "name": "#再忙碌也需要直播#",
      "pub_stat": 1,
      "room_id": 458928737,
      "share_addr": "http://live2.a8.com/s/?uid=2538608&liveid=1469356863401977&ctime=1469356863",
      "slot": 3,
      "status": 0,
      "stream_addr": "http://pull99.a8.com/live/1469356863401977.flv?ikHost=ws&ikOp=1&CodecInfo=8192",
      "version": 0,
      "online_users": 18187,
      "group": 0,
      "link": 0,
      "optimal": 0,
      "multi": 0,
      "rotate": 0
    },
    {
      "city": "郑州市",
      "creator": {
        "emotion": "单身",
        "inke_verify": 0,
        "verified": 0,
        "description": "玩往死里玩🙂",
        "gender": 0,
        "profession": "玩💃",
        "id": 7748844,
        "verified_reason": "",
        "nick": "༺姗͈̎姗͈̎来͈̎迟͈̎༻",
        "location": "郑州市",
        "birth": "1998-07-10",
        "hometown": "河南省&郑州市",
        "portrait": "MTg4MjExNDY5MjYxNTk3.jpg",
        "gmutex": 0,
        "third_platform": "0",
        "level": 71,
        "rank_veri": 10,
        "veri_info": "美人"
      },
      "id": "1469356844968217",
      "image": "",
      "name": "",
      "pub_stat": 1,
      "room_id": 458927765,
      "share_addr": "http://live2.a8.com/s/?uid=7748844&liveid=1469356844968217&ctime=1469356844",
      "slot": 1,
      "status": 0,
      "stream_addr": "http://pull99.a8.com/live/1469356844968217.flv?ikHost=ws&ikOp=1&CodecInfo=8192",
      "version": 0,
      "online_users": 17974,
      "group": 0,
      "link": 0,
      "optimal": 0,
      "multi": 0,
      "rotate": 0
    },
    {
      "city": "深圳市",
      "creator": {
        "emotion": "单身",
        "inke_verify": 1,
        "verified": 81,
        "description": "JayneSkin 杰恩护肤 八月上线 详情VX；junxuee",
        "gender": 1,
        "profession": "商业邀约➕工作VX junnannn",
        "id": 2744234,
        "verified_reason": "视频达人",
        "nick": "🦄杰恩卑鄙",
        "location": "深圳市",
        "birth": "1996-06-25",
        "hometown": "辽宁省&沈阳市",
        "portrait": "NTMwMTgxNDY5MzYyOTgx.jpg",
        "gmutex": 0,
        "third_platform": "0",
        "level": 59,
        "rank_veri": 81,
        "veri_info": "视频达人"
      },
      "id": "1469356943418419",
      "image": "",
      "name": "我要没电了",
      "pub_stat": 1,
      "room_id": 458932937,
      "share_addr": "http://live7.a8.com/s/?uid=2744234&liveid=1469356943418419&ctime=1469356943",
      "slot": 3,
      "status": 0,
      "stream_addr": "http://pull99.a8.com/live/1469356943418419.flv?ikHost=ws&ikOp=1&CodecInfo=8192",
      "version": 0,
      "online_users": 18092,
      "group": 0,
      "link": 0,
      "optimal": 0,
      "multi": 0,
      "rotate": 0
    },
    {
      "city": "杭州市",
      "creator": {
        "emotion": "保密",
        "inke_verify": 0,
        "verified": 0,
        "description": "几支玻尿酸谁和谁都像，记住我给你的感觉别人给不了",
        "gender": 0,
        "profession": "无",
        "id": 3755345,
        "verified_reason": "",
        "nick": "希雅bb✨",
        "location": "杭州市",
        "birth": "2015-01-01",
        "hometown": "火星&",
        "portrait": "MTk5NzIxNDY4OTM1Mjky.jpg",
        "gmutex": 0,
        "third_platform": "0",
        "level": 26,
        "rank_veri": 5,
        "veri_info": "小公举"
      },
      "id": "1469357103083633",
      "image": "",
      "name": "",
      "pub_stat": 1,
      "room_id": 458941711,
      "share_addr": "http://live.a8.com/s/?uid=3755345&liveid=1469357103083633&ctime=1469357103",
      "slot": 6,
      "status": 0,
      "stream_addr": "http://pull99.a8.com/live/1469357103083633.flv?ikHost=ws&ikOp=1&CodecInfo=8192",
      "version": 0,
      "online_users": 17868,
      "group": 0,
      "link": 0,
      "optimal": 0,
      "multi": 0,
      "rotate": 0
    }
  ],
  "expire_time": 15
}
```



代码示例

http://120.55.238.158/api/live/infos?imsi=&uid=150633875&proto=7&idfa=E54DF3AE-FBD1-49B0-8F26-9973BEED9404&lc=0000000000000030&cc=TG0001&imei=&sid=20bUJGsWAjuqogNFHdEA9g0rBuz39eR8x9a18ti1RTWCaIhhZi2g&cv=IK3.2.60_Iphone&devi=9f574585642d2befc53f2e53ce7cc9adbd51c8da&conn=Wifi&ua=iPhone%205s&idfv=501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1&osversion=ios_9.200000&id=1469357062262570%2C1469356863401977%2C1469356844968217%2C1469356943418419%2C1469357103083633&multiaddr=1



# api/Next

上下滑动切换主播

## URL

[http://120.55.238.158/api/live/next](http://120.55.238.158/api/live/next  )

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
| id        | true | string | 1469360028266357                         |
| multiaddr | true | string | 1                                        |
| action    | true | string | all                                      |
| latitude  | true | string | 23.173429                                |
| longitude | true | string | 113.332183                               |
| multiaddr | true | string | 1                                        |
| source    | true | string | 0                                        |
| step      | true | string | 0                                        |



## 返回结果

JSON示例

```objective-c
{
  "alive": 0,
  "dm_error": 0,
  "error_msg": "操作成功",
  "infos": [
    {
      "city": "北京市",
      "creator": {
        "emotion": "单身",
        "inke_verify": 0,
        "verified": 0,
        "description": "微博：然老爺soso。榜前6给V。qq群559240753",
        "gender": 1,
        "profession": "淘宝店名：它山小铺（主营珠宝）",
        "id": 2941547,
        "verified_reason": "",
        "nick": "然🔥",
        "location": "北京市",
        "birth": "1992-06-29",
        "hometown": "",
        "portrait": "MzQ5MzQxNDY3ODkxODM1.jpg",
        "gmutex": 0,
        "third_platform": "1",
        "level": 31,
        "rank_veri": 5,
        "veri_info": "怪蜀黍"
      },
      "id": "1469375101169637",
      "image": "",
      "name": "#再忙碌也需要直播#",
      "pub_stat": 1,
      "publish_addr": "http://link.a8.com:7788/publish/trans/inke/mlinkm/1469375101169637?ikProfile=3&ikWidth=368&ikHeight=640&ikBr=800&ikHost=pz&ikOp=1&ndselect=3",
      "room_id": 460018554,
      "share_addr": "http://live7.a8.com/s/?uid=2941547&liveid=1469375101169637&ctime=1469375101",
      "slot": 6,
      "status": 1,
      "stream_addr": "http://pull99.a8.com/live/1469375101169637.flv?ikHost=ws&ikOp=1&CodecInfo=8192",
      "version": 0,
      "link": 0,
      "optimal": 0,
      "multi": 0,
      "rotate": 0
    }
  ]
}
```

代码示例:

http://120.55.238.158/api/live/next?imsi=&uid=150633875&proto=7&idfa=E54DF3AE-FBD1-49B0-8F26-9973BEED9404&lc=0000000000000030&cc=TG0001&imei=&sid=20bUJGsWAjuqogNFHdEA9g0rBuz39eR8x9a18ti1RTWCaIhhZi2g&cv=IK3.2.60_Iphone&devi=9f574585642d2befc53f2e53ce7cc9adbd51c8da&conn=Wifi&ua=iPhone%205s&idfv=501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1&osversion=ios_9.200000&action=all&id=1469360028266357&latitude=23.173429&longitude=113.332183&multiaddr=1&source=0&step=0





# api/FriendList

关注列表

## URL

[http://120.55.238.158/api/live/friendlist](http://120.55.238.158/api/live/friendlist  )

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
  "expire_time": 60,
  "friends": []
}
```



借口示例

http://120.55.238.158/api/live/friendlist?imsi=&uid=150633875&proto=7&idfa=E54DF3AE-FBD1-49B0-8F26-9973BEED9404&lc=0000000000000030&cc=TG0001&imei=&sid=20bUJGsWAjuqogNFHdEA9g0rBuz39eR8x9a18ti1RTWCaIhhZi2g&cv=IK3.2.60_Iphone&devi=9f574585642d2befc53f2e53ce7cc9adbd51c8da&conn=Wifi&ua=iPhone%205s&idfv=501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1&osversion=ios_9.200000&



# api/Ticker

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



# api/Chat

聊天

## URL

[http://120.55.238.158/api/chat/iplist](http://120.55.238.158/api/chat/iplist  )

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
  "cfg": [
    {
      "slot": 1,
      "addr": "60.205.82.63:81|60.205.82.60:81"
    },
    {
      "slot": 2,
      "addr": "60.205.82.51:81|60.205.82.46:81"
    },
    {
      "slot": 3,
      "addr": "60.205.82.41:81|60.205.82.39:81"
    },
    {
      "slot": 4,
      "addr": "60.205.82.30:81|60.205.82.33:81"
    },
    {
      "slot": 5,
      "addr": "60.205.82.22:81|60.205.82.14:81"
    },
    {
      "slot": 6,
      "addr": "60.205.82.10:81|101.201.58.184:81"
    }
  ],
  "error_msg": "操作成功",
  "dm_error": 0
}
```

示例

http://120.55.238.158/api/chat/iplist?imsi=&uid=150633875&proto=7&idfa=E54DF3AE-FBD1-49B0-8F26-9973BEED9404&lc=0000000000000030&cc=TG0001&imei=&sid=20bUJGsWAjuqogNFHdEA9g0rBuz39eR8x9a18ti1RTWCaIhhZi2g&cv=IK3.2.60_Iphone&devi=9f574585642d2befc53f2e53ce7cc9adbd51c8da&conn=Wifi&ua=iPhone%205s&idfv=501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1&osversion=ios_9.200000

# api/User

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



# api/User

账户信息

## URL

[http://120.55.238.158/api/user/info](http://120.55.238.158/api/user/info  )

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
| id        | true | string | 150633875                                |



## 返回结果

JSON示例

```objective-c
{
  "dm_error": 0,
  "error_msg": "操作成功",
  "user": {
    "emotion": "",
    "inke_verify": 0,
    "verified": 0,
    "description": "",
    "gender": 1,
    "profession": "",
    "third_platform": "0",
    "verified_reason": "",
    "nick": "Sun",
    "location": "广州市",
    "birth": "",
    "hometown": "",
    "portrait": "MzE3NDAxNDQ1Mzk1MTkx.jpg",
    "gmutex": 0,
    "id": 150633875,
    "level": 3,
    "rank_veri": 3,
    "veri_info": ""
  }
}
```

示例

http://120.55.238.158/api/user/info?imsi=&uid=150633875&proto=7&idfa=E54DF3AE-FBD1-49B0-8F26-9973BEED9404&lc=0000000000000030&cc=TG0001&imei=&sid=20bUJGsWAjuqogNFHdEA9g0rBuz39eR8x9a18ti1RTWCaIhhZi2g&cv=IK3.2.60_Iphone&devi=9f574585642d2befc53f2e53ce7cc9adbd51c8da&conn=Wifi&ua=iPhone%205s&idfv=501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1&osversion=ios_9.200000&id=150633875



# api/Inout

gold和point数量

## URL

[http://120.55.238.158/api/statistic/inout](http://120.55.238.158/api/statistic/inout  )

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
| id        | true | string | 8540029(所查的用户ID)                         |



## 返回结果

JSON示例

```objective-c
{
  "error_msg": "操作成功",
  "inout": {
    "gold": 90848,
    "point": 2526352
  },
  "dm_error": 0
}
```



示例

http://120.55.238.158/api/statistic/inout?imsi=&uid=150633875&proto=7&idfa=E54DF3AE-FBD1-49B0-8F26-9973BEED9404&lc=0000000000000030&cc=TG0001&imei=&sid=20bUJGsWAjuqogNFHdEA9g0rBuz39eR8x9a18ti1RTWCaIhhZi2g&cv=IK3.2.60_Iphone&devi=9f574585642d2befc53f2e53ce7cc9adbd51c8da&conn=Wifi&ua=iPhone%205s&idfv=501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1&osversion=ios_9.200000&id=8540029

请求方法:

```objective-c
- (void)sendRequest:(id)sender
{
    /* Configure session, choose between:
       * defaultSessionConfiguration
       * ephemeralSessionConfiguration
       * backgroundSessionConfigurationWithIdentifier:
     And set session-wide properties, such as: HTTPAdditionalHeaders,
     HTTPCookieAcceptPolicy, requestCachePolicy or timeoutIntervalForRequest.
     */
    NSURLSessionConfiguration* sessionConfig = [NSURLSessionConfiguration defaultSessionConfiguration];
 
    /* Create session, and optionally set a NSURLSessionDelegate. */
    NSURLSession* session = [NSURLSession sessionWithConfiguration:sessionConfig delegate:nil delegateQueue:nil];

    /* Create the Request:
       My API (GET http://120.55.238.158/api/statistic/inout)
     */

    NSURL* URL = [NSURL URLWithString:@"http://120.55.238.158/api/statistic/inout"];
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
        @"id": @"8540029",
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

# api/Tips

15个提示

## URL

[http://120.55.238.158/api/live/tips](http://120.55.238.158/api/live/tips  )

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
| uid       | true | string | 0                                        |
| imsi      | true | string | 空值                                       |
| proto     | true | string | 7                                        |
| idfa      | true | string | E54DF3AE-FBD1-49B0-8F26-9973BEED9404     |
| lc        | true | string | 0000000000000030                         |
| cc        | true | string | TG0001                                   |
| imei      | true | string | 空值                                       |
| sid       | true | string | 空值                                       |
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
  "tips": [
    {
      "content": "你丑你先睡，我美我直播！[直播ing] ＃{$livename}＃",
      "type": "qq",
      "title": "你丑你先睡，我美我直播！"
    },
    {
      "content": "你丑你先睡，我美我直播！[直播ing]＃{$livename}＃，点此进入>> {$shareurl}",
      "type": "weibo",
      "title": "你丑你先睡，我美我直播！"
    },
    {
      "content": "你丑你先睡，我美我直播！{$nickname}正在直播，速来围观~",
      "type": "qzone_noname",
      "title": "你丑你先睡，我美我直播！"
    },
    {
      "content": "复制整段信息，打开［映客］可直接看直播，{$nickname}正在{$city}直播 {$livename}🔑{$liveid}🔑还没安装映客？点此安装，http://inke.tv",
      "type": "inke_signal",
      "title": ""
    },
    {
      "content": "我们提倡纯净健康直播，严禁色情、政治、宗教、赌博等违法或低俗、暴露、挑逗性内容及直播封面、头像、用户名，一经发现将封停账号",
      "type": "start_broadcast",
      "title": ""
    },
    {
      "content": "你丑你先睡，我美我直播！{$nickname}正在[直播]，速来围观",
      "type": "qq_noname",
      "title": "你丑你先睡，我美我直播！"
    },
    {
      "content": "你丑你先睡，我美我直播！{$nickname}正在直播，快来一起看~",
      "type": "wxfriends_noname",
      "title": "你丑你先睡，我美我直播！"
    },
    {
      "content": "你丑你先睡，我美我直播！{$nickname}正在直播，快来一起看~",
      "type": "wxfriends",
      "title": "你丑你先睡，我美我直播！"
    },
    {
      "content": "{\"desc\": \"充值问题，点此联系客服\", \"link\": \"http://kefu.easemob.com/webim/im.html?tenantId=13765\"}",
      "type": "payment_feedback",
      "title": "充值页面失败引导"
    },
    {
      "content": "你丑你先睡，我美我直播！{$nickname}正在直播，速来围观，点此进入>> {$shareurl}",
      "type": "weibo_noname",
      "title": "你丑你先睡，我美我直播！"
    },
    {
      "content": "你丑你先睡，我美我直播！{$nickname}正在直播，快来一起看~",
      "type": "wechat",
      "title": "你丑你先睡，我美我直播！"
    },
    {
      "content": "复制整段信息，打开［映客］可直接看直播，{$nickname}邀请你来看他的私密直播#{$livename}🔑{$liveid}🔑还没安装映客？点此安装，http://inke.tv",
      "type": "inke_private_signal",
      "title": ""
    },
    {
      "content": "你丑你先睡，我美我直播！[直播ing] ＃{$livename}＃",
      "type": "qzone",
      "title": "你丑你先睡，我美我直播！"
    },
    {
      "content": "你丑你先睡，我美我直播！{$nickname}正在直播，快来一起看~",
      "type": "wechat_noname",
      "title": "你丑你先睡，我美我直播！"
    },
    {
      "content": "请升级新版欣赏礼物",
      "type": "git_effect_not_supported",
      "title": ""
    }
  ],
  "error_msg": "操作成功",
  "dm_error": 0
}
```



示例

http://120.55.238.158/api/live/tips?imsi=&uid=0&proto=7&idfa=E54DF3AE-FBD1-49B0-8F26-9973BEED9404&lc=0000000000000030&cc=TG0001&imei=&sid=&cv=IK3.2.60_Iphone&devi=9f574585642d2befc53f2e53ce7cc9adbd51c8da&conn=Wifi&ua=iPhone%205s&idfv=501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1&osversion=ios_9.200000





# api/SimpleAll

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



# api/Gift

礼物

## URL

[http://120.55.238.158/api/resource/gift_info](http://120.55.238.158/api/resource/gift_info  )

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
| uid       | true | string | 0                                        |
| imsi      | true | string | 空值                                       |
| proto     | true | string | 7                                        |
| idfa      | true | string | E54DF3AE-FBD1-49B0-8F26-9973BEED9404     |
| lc        | true | string | 0000000000000030                         |
| cc        | true | string | TG0001                                   |
| imei      | true | string | 空值                                       |
| sid       | true | string | 空值                                       |
| cv        | true | string | IK3.2.60_Iphone                          |
| devi      | true | string | 9f574585642d2befc53f2e53ce7cc9adbd51c8da |
| conn      | true | string | Wifi                                     |
| ua        | true | string | iPhone%205s                              |
| idfv      | true | string | 501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1     |
| osversion | true | string | ios_9.200000                             |
| scale     | true | string | 2                                        |
| type      | true | string | 2                                        |



## 返回结果

JSON示例

```objective-c
{
  "gifts": [
    {
      "name": "小火炬",
      "gold": 2,
      "cl": [
        111,
        111,
        111
      ],
      "image": "MzYxMTcxNDY5MTc1ODQw.jpg",
      "exp": 20,
      "type": 1,
      "id": 158,
      "icon": "MTA0NDMxNDY5MTc1ODEz.jpg"
    },
    {
      "name": "小黄瓜",
      "gold": 1,
      "cl": [
        255,
        255,
        255
      ],
      "image": "NTYyMTgxNDQ3MTQ0NDcw.jpg",
      "exp": 10,
      "type": 1,
      "id": 73,
      "icon": "MzEzNDIxNDQ3MTQzNzM4.jpg"
    },
    {
      "name": "樱花雨",
      "gold": 1,
      "cl": [
        255,
        255,
        255
      ],
      "image": "OTc4MzYxNDUxODkzMDk4.jpg",
      "exp": 10,
      "type": 1,
      "id": 131,
      "icon": "NTg4MzMxNDUxODkzMDkw.jpg"
    },
    {
      "name": "心花怒放",
      "gold": 10,
      "cl": [
        165,
        165,
        165
      ],
      "image": "MzE5MDkxNDY5MTgyMzcx.jpg",
      "exp": 100,
      "type": 1,
      "id": 160,
      "icon": "MzA4ODQxNDY5MTgyNzk4.jpg"
    },
    {
      "name": "小映金牌",
      "gold": 188,
      "cl": [
        163,
        163,
        163
      ],
      "image": "MTQwNjMxNDY5MTc3MzQ1.jpg",
      "exp": 1880,
      "type": 1,
      "id": 159,
      "icon": "MTgwMTQxNDY5MTc3MzE5.jpg"
    },
    {
      "name": "保时捷",
      "gold": 1200,
      "cl": [
        255,
        255,
        255
      ],
      "image": "MjkyNzgxNDQ2MjA0NTYz.jpg",
      "exp": 12000,
      "type": 2,
      "id": 65,
      "icon": "MzA5NTIxNDQ2MDg4ODU5.jpg"
    },
    {
      "name": "皇家游轮",
      "gold": 13140,
      "cl": [
        255,
        255,
        255
      ],
      "image": "NTgxNjAxNDU0Mzk0Nzc4.jpg",
      "exp": 131400,
      "type": 2,
      "id": 132,
      "icon": "MTA1MDMxNDU0Mzk0NzY3.jpg"
    },
    {
      "name": "陪你看海",
      "gold": 33440,
      "cl": [
        244,
        232,
        232
      ],
      "image": "NDE1MTcxNDY3OTU4MDYw.jpg",
      "exp": 334400,
      "type": 2,
      "id": 155,
      "icon": "NTUxNTcxNDY3OTU4MDQ2.jpg"
    },
    {
      "name": "大西瓜",
      "gold": 1,
      "cl": [
        221,
        211,
        222
      ],
      "image": "MzQ0MTExNDY2NDc3OTY1.jpg",
      "exp": 10,
      "type": 1,
      "id": 154,
      "icon": "Mjk4ODQxNDY2NDc3OTQw.jpg"
    },
    {
      "name": "小香蕉",
      "gold": 2,
      "cl": [
        255,
        255,
        255
      ],
      "image": "Mjg0MjMxNDQ4MzM4Njky.jpg",
      "exp": 20,
      "type": 1,
      "id": 108,
      "icon": "MzUxODQxNDQ4MzM4Njgz.jpg"
    },
    {
      "name": "荧光棒",
      "gold": 2,
      "cl": [
        255,
        255,
        255
      ],
      "image": "ODUzMzcxNDUwMTgwMjkx.jpg",
      "exp": 20,
      "type": 1,
      "id": 112,
      "icon": "MjU1MjUxNDUwMTgwMjM2.jpg"
    },
    {
      "name": "玫瑰花",
      "gold": 10,
      "cl": [
        255,
        255,
        255
      ],
      "image": "NTE1NzIxNDU0NjYwOTEy.jpg",
      "exp": 100,
      "type": 1,
      "id": 138,
      "icon": "NDE2NDcxNDU0NjYwOTAy.jpg"
    },
    {
      "name": "爱の礼花",
      "gold": 6666,
      "cl": [
        255,
        255,
        255
      ],
      "image": "NzM3NDYxNDU0Mzk0OTI2.jpg",
      "exp": 66660,
      "type": 2,
      "id": 133,
      "icon": "NDAyNzcxNDU0Mzk1MDQz.jpg"
    },
    {
      "name": "钻戒",
      "gold": 199,
      "cl": [
        255,
        255,
        255
      ],
      "image": "MzM3NjMxNDQ3MTQ1Mjk0.jpg",
      "exp": 1990,
      "type": 1,
      "id": 105,
      "icon": "MTY0MjIxNDQ3MTQ1MDQ1.jpg"
    },
    {
      "name": "任性红包",
      "gold": 3000,
      "cl": [
        255,
        255,
        255
      ],
      "image": "ODg4MTUxNDQ5OTI0MTIy.jpg",
      "exp": 30000,
      "type": 3,
      "id": 111,
      "icon": "NTcyODUxNDQ5OTI0MTA4.jpg"
    },
    {
      "name": "霓虹超跑",
      "gold": 6666,
      "cl": [
        255,
        255,
        255
      ],
      "image": "Njg1MzUxNDQ4ODcxNDcz.jpg",
      "exp": 66660,
      "type": 2,
      "id": 110,
      "icon": "OTY1MTkxNDQ4ODcxNDQz.jpg"
    },
    {
      "name": "大蘑菇",
      "gold": 1,
      "cl": [
        255,
        255,
        255
      ],
      "image": "NTk3NTIxNDUwNzAyMDcw.jpg",
      "exp": 10,
      "type": 1,
      "id": 116,
      "icon": "NTQxMjIxNDUwNzAyMTAz.jpg"
    },
    {
      "name": "大啤酒",
      "gold": 2,
      "cl": [
        255,
        245,
        245
      ],
      "image": "MTkwOTQxNDUxNTcxMjI2.jpg",
      "exp": 20,
      "type": 1,
      "id": 128,
      "icon": "NTYxMjUxNDUxNTcxMjEx.jpg"
    },
    {
      "name": "单身狗",
      "gold": 5,
      "cl": [
        255,
        255,
        255
      ],
      "image": "NDUxODExNDU0NjYwODA1.jpg",
      "exp": 50,
      "type": 1,
      "id": 137,
      "icon": "NDI1NjkxNDU0NjYwNjU1.jpg"
    },
    {
      "name": "么么哒",
      "gold": 33,
      "cl": [
        255,
        255,
        255
      ],
      "image": "MjE3NDgxNDY0NjYzNTQz.jpg",
      "exp": 330,
      "type": 1,
      "id": 103,
      "icon": "MjgyMDUxNDY0NjYzNTM3.jpg"
    },
    {
      "name": "粉钻",
      "gold": 88,
      "cl": [
        255,
        255,
        255
      ],
      "image": "MjA2NzExNDQ3MTQ1NTY2.jpg",
      "exp": 880,
      "type": 1,
      "id": 107,
      "icon": "NDQ3MTMxNDQ3MTQ1NTUz.jpg"
    },
    {
      "name": "红包",
      "gold": 500,
      "cl": [
        255,
        255,
        255
      ],
      "image": "NTI5NTIxNDUwOTM5MTIz.jpg",
      "exp": 5000,
      "type": 3,
      "id": 126,
      "icon": "MTM4NTUxNDUwOTM5MDYw.jpg"
    },
    {
      "name": "飞机",
      "gold": 3000,
      "cl": [
        255,
        255,
        255
      ],
      "image": "MzI5ODUxNDQ2MDIyNDcy.jpg",
      "exp": 30000,
      "type": 2,
      "id": 69,
      "icon": "MjM3NjIxNDQ2MTAwNjA3.jpg"
    },
    {
      "name": "法拉利",
      "gold": 3000,
      "cl": [
        255,
        255,
        255
      ],
      "image": "ODE1OTUxNDQ2MDIyMjMy.jpg",
      "exp": 30000,
      "type": 2,
      "id": 67,
      "icon": "MTk5MTIxNDQ2MDg4ODcy.jpg"
    },
    {
      "name": "手枪",
      "gold": 2,
      "cl": [
        255,
        255,
        255
      ],
      "image": "NzE3MjYxNDUwNzAyMjk1.jpg",
      "exp": 20,
      "type": 1,
      "id": 118,
      "icon": "MjIyMDgxNDUwNzAyMjgx.jpg"
    },
    {
      "name": "爱の皮鞭",
      "gold": 3,
      "cl": [
        225,
        255,
        255
      ],
      "image": "MzEyODExNDUwOTM2NzYx.jpg",
      "exp": 30,
      "type": 1,
      "id": 123,
      "icon": "NjI1NjgxNDUwOTM2NzUw.jpg"
    },
    {
      "name": "爱的抱抱",
      "gold": 5,
      "cl": [
        255,
        255,
        255
      ],
      "image": "Mzk2MDUxNDUwMTgwNzIw.jpg",
      "exp": 50,
      "type": 1,
      "id": 114,
      "icon": "MTkyNjkxNDUwMTgwNjcw.jpg"
    },
    {
      "name": "蛋糕",
      "gold": 10,
      "cl": [
        220,
        72,
        72
      ],
      "image": "Mjk2MTkxNDQ2MDIyMzUy.jpg",
      "exp": 100,
      "type": 1,
      "id": 61,
      "icon": "NzkwMjkxNDQ2MDg4NjE0.jpg"
    }
  ],
  "error_msg": "操作成功",
  "dm_error": 0
}
```



示例

http://120.55.238.158/api/resource/gift_info?imsi=&uid=0&proto=7&idfa=E54DF3AE-FBD1-49B0-8F26-9973BEED9404&lc=0000000000000030&cc=TG0001&imei=&sid=&cv=IK3.2.60_Iphone&devi=9f574585642d2befc53f2e53ce7cc9adbd51c8da&conn=Wifi&ua=iPhone%205s&idfv=501D5DCE-1DB5-4F1C-9D96-CD31D8E8D0F1&osversion=ios_9.200000&scale=2&type=2

```

```




