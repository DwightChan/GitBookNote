[toc]

---


# React Native指定设备运行

>  原文：[http://blog.csdn.net/u010359739/article/details/71221309](https://link.jianshu.com/?t=http://blog.csdn.net/u010359739/article/details/71221309)
> React Native运行项目会自动启动模拟器或者真机，下面为指定启动模拟器的方法

```
注意：运行项目之前执行npm install是必须的
```

## 1. Android

Android运行React Native项目有两种方式：

### 1.1 终端

命令行中React native项目目录下键入react-native run-android会启动当前电脑连接的Android设备

```
查看Android设备：在终端中输入adb devices
```

若未展示电脑连接Android设备信息，就是adb环境配置有问题，可按需配置Android环境变量

命令行中启动Android模拟器可参考：

[http://blog.csdn.net/u010359739/article/details/54708960](https://link.jianshu.com/?t=http://blog.csdn.net/u010359739/article/details/54708960)

### 1.2 IDE

使用Android Studio打开React Native项目，点击Run运行项目

## 2. iOS

### 2.1 终端

命令行中React native项目目录下键入react-native run-ios会启动iOS模拟器，默认是使用iPhone6，如果想要试用其他版本的模拟器则需要在react-native run-ios后携带参数–simulator

启动iPhone7：`react-native run-ios --simulator "iPhone 7 Plus”`

—-simulator后指定模拟器的名字

```
查看iOS设备：在终端中输入xcrun simctl list devices
```

若已经打开了一个模拟器，需要先关闭这个模拟器，再执行react-native run-ios命令打开的就是新的模拟器

### 1.2 IDE

打开React Native项目目录下iOS目录下的Xcode工程，然后在工程中点击运行按钮，运行设备或模拟器可在Xcode中对应选择

## 参考链接：

React Native官网：[https://facebook.github.io/react-native/](https://link.jianshu.com/?t=https://facebook.github.io/react-native/)

React Native中文网：[https://reactnative.cn/](https://link.jianshu.com/?t=https://reactnative.cn/)