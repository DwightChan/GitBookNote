# api/live/next

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




