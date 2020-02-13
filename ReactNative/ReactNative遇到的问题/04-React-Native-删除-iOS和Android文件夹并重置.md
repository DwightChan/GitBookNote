[toc]



---

# React-Native-删除-iOS和Android文件夹并重置

> 原创fateofkingdom 最后发布于2019-10-17 08:59:59 阅读数 122  收藏

首先把iOS和Android 文件夹删除，最好是改个名字备份一下。
然后用终端进入项目根目录。
输入
```
react-native upgrade --legacy true
```
然后建立连接
```
react-native link
```
如果有手动添加东西，比如: 用了**iconfont，就要手动重新添加**。
如果依赖库有问题，那就把node_modules文件夹删除，
然后
```
npm install
```
————————————————
> 版权声明：本文为CSDN博主「fateofkingdom」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/yanhuoai/article/details/102584026