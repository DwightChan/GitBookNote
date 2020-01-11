# AccessToken

## 课程目标

* 自定义对象
* 构造函数
* 归档 & 接档

## 接口定义

### 文档地址

http://open.weibo.com/wiki/OAuth2/access_token

### 接口地址

https://api.weibo.com/oauth2/access_token

### HTTP 请求方式

* POST

### 请求参数

| 参数 | 描述 |
| -- | -- |
| client_id | 申请应用时分配的AppKey |
| client_secret | 申请应用时分配的AppSecret |
| grant_type | 请求的类型，填写 `authorization_code` |
| code | 调用authorize获得的code值 |
| redirect_uri | 回调地址，需需与注册应用里的回调地址一致 |

### 返回数据

| 返回值字段 | 字段说明 |
| -- | -- |
| access_token | 用于调用access_token，接口获取授权后的access token |
| expires_in | access_token的生命周期，单位是秒数 |
| remind_in | access_token的生命周期（该参数即将废弃，开发者请使用expires_in） |
| uid | 当前授权用户的UID |


