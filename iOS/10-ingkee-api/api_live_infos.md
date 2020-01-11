# api/live/infos

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


