

# api/resource/gift_info

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

