# React-native 中使用 react-native-vector-icons 图标库

> CONS是矢量图，可以直接使用图片名, 就能加载图片的第三方,使用很方便, 你不需要在工程文件夹里塞各种图片, 字体图标的使用在开发中常常有意想不到的趣味性，和便捷而且大小颜色等定义相对于图片而言实在是方便不少；
>
> 刚入RN 不久今天遇到了点坑，现在分享总结一下 react-native-vector-icons的简单使用，虽然之前也看了需要地方的教程，但是可能因为版本的原因，运行项目都是包无法加载字体文件；本文所在系统 为 IOS下，
>
> - 初始化 React-native 项目工程，还不会的同学可以参考一下，[RN 中文网](http://reactnative.cn/docs/0.48/getting-started.html#content)
> - 项目初始化完成后进入当前项目 安装字体图标库 ，终端中运行
>   npm install react-native-vector-icons --save 回车下载安装依赖包
> - 打开x-code 打开RN 项目里面的IOS 文件下面的 x-code 文件



![image.png](https://user-gold-cdn.xitu.io/2017/11/12/af671647e3108d58f626cbdb7bfdf3ef?imageView2/0/w/1280/h/960/ignore-error/1)image.png



> 点击当前文件 右键添加下载好的 react-native-vector-icons 字体图标文件



![image.png](https://user-gold-cdn.xitu.io/2017/11/12/51904c3dc51be78102f039410bef882d?imageView2/0/w/1280/h/960/ignore-error/1)image.png



> 添加 字体文件到当前项目，选择如下
> 路径大概是这样的： RN项目/node_modules/react-native-vector-icons/Fonts



![image.png](https://user-gold-cdn.xitu.io/2017/11/12/73edfe33075ca46a9a9d991dd1973f52?imageView2/0/w/1280/h/960/ignore-error/1)image.png



> - 回到当前RN 项目下，使用 rnpm 让刚才添加的字体文件关联到RN项目中使用（使其资源[user-gold-cdn.xitu.io/2017/11/12/…](https://user-gold-cdn.xitu.io/2017/11/12/f84703dec971adb2385d6756dec98ba9Xcode进行连接），如果没有) 安装rnpm 可以使用 sudo npm install rnpm -g 安装 安装完成后 rnpm -V 查看是否安装成功，成功则会显示对应的版本号，运行 rnpm link ，等待关联成功



![image.png](https://user-gold-cdn.xitu.io/2017/11/12/ac364c41f57e0aff6ae76c12ea822df5?imageView2/0/w/1280/h/960/ignore-error/1)image.png



> 这个时候你可以到x -code 中查看字体资源是否已经加载到项目中了(这里指的是fonts是否有包含)
> 下面这个图中 info.plist 文件中要手动添加字段 Fonts provided by application;
> 要手动给 Fonts provided by application 字段添加对应的 item并把 对应要添加的字体库作为item 的值;



![image.png](https://user-gold-cdn.xitu.io/2017/11/12/a61711afc9afe25dd2918bdad038b655?imageView2/0/w/1280/h/960/ignore-error/1)image.png



- 到这来我们已经可以任意的使用字体图标了，项目中

  ```
  //引用
  import Ionicons from "react-native-vector-icons/Ionicons";
  // 使用
  <Ionicons name={ "ios-home" }   size={26}/>复制代码
  ```

  ![image.png](https://user-gold-cdn.xitu.io/2017/11/12/2bf7c55c5b44a84728f3ec00a4c99509?imageView2/0/w/1280/h/960/ignore-error/1)image.png

> 到此教程就完毕了，总结一下，只要注意一下顺序，并不像其他教程一下需要在x-code 的 info 中一一去加关联的字体，理论上只要 react-native-vector-icons 支持的图标库都可以通过这样的方式快速导入使用，当然有人问了: 那对应的图标的名称怎么查询 ？
>
> 就支持的 [Font Awesome](http://fontawesome.io/)为例子



![image.png](data:image/svg+xml;utf8,<?xml%20version=%221.0%22?%3E%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20version=%221.1%22%20width=%22800%22%20height=%22600%22%3E%3C/svg%3E)image.png



```
//引用
import FontAwesome from "react-native-vector-icons/FontAwesome";
// 使用（可能需求去掉 字体名称前缀 这里是 fa）
<FontAwesome name={ "address-book" }   size={26}/>复制代码
```



![image.png](data:image/svg+xml;utf8,<?xml%20version=%221.0%22?%3E%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20version=%221.1%22%20width=%22736%22%20height=%22122%22%3E%3C/svg%3E)image.png



> 至于其他的图标库，也是类似再举个[ionicons](http://ionicons.com/) 的🌰
> 到官网找到你需要的字体图标 



![image.png](data:image/svg+xml;utf8,<?xml%20version=%221.0%22?%3E%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20version=%221.1%22%20width=%221240%22%20height=%22936%22%3E%3C/svg%3E)image.png



```
//引用
import Ionicons from "react-native-vector-icons/Ionicons";
// 使用 （需要把 ion-ionic 修改成 ios- ionic ）
<Ionicons name={ "ios- ionic" }   size={26}/>复制代码
```



![image.png](https://user-gold-cdn.xitu.io/2017/11/12/e7bffe573c95cd316ddba7f94c2683f6?imageView2/0/w/1280/h/960/ignore-error/1)image.png



> 至于其他的同理，大家多去尝试一下就可以了，字体库都关联到项目了，怎么用多多尝试就好，其实大概是这样的修改名字，我也只是猜测，没想到果然如此；当然可以自定义图标库，关联使用；
>
> 如果觉得不错，路过不要忘记点赞哦 敏呐~~

原文链接([www.jianshu.com/p/91affb41a…](http://www.jianshu.com/p/91affb41a075))

关注下面的标签，发现更多相似文章

[React.js](https://juejin.im/tag/React.js)[图片资源](https://juejin.im/tag/图片资源)[Icon](https://juejin.im/tag/Icon)[前端](https://juejin.im/tag/前端)









[捏泥巴的小人](https://juejin.im/user/58afec7d8d6d81005854be71)[![lv-1](https://b-gold-cdn.xitu.io/v3/static/img/lv-1.636691c.svg)](https://juejin.im/book/5c90640c5188252d7941f5bb/section/5c9065385188252da6320022)web开发

[发布了 5 篇专栏 · ](https://juejin.im/user/58afec7d8d6d81005854be71/posts)获得点赞 52 · 获得阅读 4,532

关注