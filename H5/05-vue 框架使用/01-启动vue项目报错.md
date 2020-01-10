

[toc]

<hr/>
# 启动vue项目报错

## 启动vue项目报错 these dependencies were not found:element-ui in ./src/main.js

###  **错误信息如下**

![](https://img-blog.csdnimg.cn/20190508172411702.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM3NTkxNjM3,size_16,color_FFFFFF,t_70)



### **解决方案**

缺少组件，在这个项目的目录下，安装组件

我之前安装过了，但是这个安装是在c盘管理员的目录下面进行的

1、使用cmd命令切换到项目的目录下面

2、cnpm i element-ui -S 如果没有使用淘宝镜像的就使用npm i element-ui -S命令

<hr/>

> 版权声明：本文为CSDN博主「WinstonLau」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
> 原文链接：https://blog.csdn.net/qq_37591637/article/details/89963361