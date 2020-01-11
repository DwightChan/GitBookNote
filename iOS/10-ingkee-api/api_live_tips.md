# api/live/tips

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



