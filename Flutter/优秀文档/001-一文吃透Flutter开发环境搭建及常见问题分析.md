[toc]

----

# **一文吃透Flutter开发环境搭建及常见问题分析**

2021.01.10 20:11 1771浏览

举报

> WARNING:内容较长建议收藏，以便后续的查找和学习。

![图片描述](https://img1.sycdn.imooc.com/5ffaeec50001e89c12800720.jpg)

跨平台技术现已成为企业提升研发效率和动态化能力，抢占新赛道的搏击场。从闲鱼到淘宝，从QQ到微信，从京东到百度，从美团到抖音，BAT等一线互联网大厂在全面拥抱Flutter。
2020 短短一年里，Flutter在GitHub 和 StackOverflow已经赶超React Native成为开发者首选跨平台框架。

> 作为想学习[Flutter开发](https://coding.imooc.com/class/321.html)或者初入Flutter开发的小伙伴该如何搭建Flutter开发环境？以及环境搭建过程中都有哪些坑？那么，在这篇文章中我将详细的向小伙伴分享Flutter开发环境搭建的经验、心得已及常见问题的分析和解决方案。

## 目录

- 在Windows上搭建Flutter开发环境
- 在Mac上搭建Flutter开发环境
- FAQ

## 在Windows上搭建Flutter开发环境

- 系统要求
- 设置Flutter镜像(非必须)
- 获取Flutter SDK
- Android开发环境设置
- 安装Flutter插件

### 系统要求

在Windows上要安装并运行Flutter要满足以下最低要求:

- 操作系统: Windows 7 SP1或更新版本
- 磁盘空间: 400 MB (不包括IDE/tools的磁盘空间）.
- 工具: Flutter 依赖下面这些命令行工具：
  - [Windows PowerShell 5.0](https://docs.microsoft.com/en-us/powershell/scripting/setup/installing-windows-powershell) Windows 10已经预装了这个工具；
  - [Git for Windows 2.x](https://git-scm.com/download/win)确保Windows电脑下载并安装了Git工具；

### 设置FLutter镜像(非必须)

由于在国内访问Flutter可能会受到限制，Flutter官方为中国开发者搭建了临时镜像，大家可以将如下环境变量加入到用户环境变量中：

```bash
PUB_HOSTED_URL=https://pub.flutter-io.cn  
FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn  
```

注意：此镜像为临时镜像，并不能保证一直可用，大家可以从 [Using Flutter in China](https://flutter.dev/community/china) 上获得有关镜像服务器的最新动态。

### 获取Flutter SDK

**1.点[Flutter官网](https://flutter.dev/docs/development/tools/sdk/archive)下载其最新可用的安装包。**

**2.解压安装包到你想安装的目录，如：`C:\flutter`；**

> 注意，不要将flutter安装到需要一些高权限的路径如`C:\Program Files\`等。

#### 设置环境变量

要在终端运行 flutter 命令， 你需要添加以下环境变量到系统`PATH`：

- 在Windows的Start 的搜索条中搜索`env`，选择`编辑帐户的环境变量`；
- 在“用户变量”下检查是否有名为“Path”的条目:
  - 如果该条目存在, 追加 `flutter\bin`的全路径，使用 ; 作为分隔符.
  - 如果条目不存在, 创建一个新用户变量 Path ，然后将 `flutter\bin`的全路径作为它的值.
- 重启Windows以应用此更改；

![img](https://img3.sycdn.imooc.com/5ffaedb60001dce413621032.jpg)
接下来，你就可以在Flutter命令行运行flutter命令了。

#### 运行 flutter doctor

上面path配置完成之后，打开一个新的命令提示符或`PowerShell`窗口并运行以下命令以查看是否需要安装任何依赖项来完成安装：

```bash
$ flutter doctor  
```

该命令检查你的环境并在终端窗口中显示报告。Dart SDK已经在捆绑在Flutter里了，没有必要单独安装Dart。 仔细检查命令行输出以获取可能需要安装的其他软件或进一步需要执行的任务（以粗体显示）：

例如：

```
[-] Android toolchain - develop for Android devices  
    • Android SDK at /Users/obiwan/Library/Android/sdk  
    ✗ Android SDK is missing command line tools; download from https://goo.gl/XxQghQ  
    • Try re-installing or updating your Android SDK,  
      visit https://flutter.dev/setup/#android-setup for detailed instructions.  
```

一般的错误会是Android Studio版本太低、或者没有`ANDROID_HOME`环境变量等

> 第一次运行一个flutter命令（如flutter doctor）时，它会下载它自己的依赖项并自行编译。以后再运行就会快得多。

### Android开发环境设置

#### 安装Android Studio

**1.下载并安装 [Android Studio](https://developer.android.com/studio)**

- https://developer.android.com/studio
- https://developer.android.google.cn/studio

> 因为Android网站设在国外，如果你的网络无法访问第一个地址，可以选择使用Google为中国开发者提供的中国网址进行访问。

另外，关于Android Studio的安装和配置，Android官方有比较详细的说明文档https://developer.android.google.cn/studio/intro，大家可以根据需要进行查阅；

> 大家在安装过程中遇到问题无法解决的，可以在我们课程的[问答区提问](https://coding.imooc.com/class/321.html)进行[提问](https://coding.imooc.com/class/321.html)；

**2.启动Android Studio，然后执行“Android Studio安装向导”。这将安装最新的Android SDK，Android SDK平台工具和Android SDK构建工具**

#### Flutter插件安装

- 打开Android Studio
- 打开Preferences > Plugins (macOS), File > Settings > Plugins (Windows & Linux)
- 选择 Browse repositories, 搜索 Flutter plugin
- 然后点击安装，然后安装Dart插件
- 完成之后选择重启Android Studio

#### 如何在Android模拟器上运行Flutter？

要准备在Android模拟器上运行并测试您的Flutter应用，需要按照以下步骤操作：

- 在你的机器上启用 [VM acceleration](https://developer.android.com/studio/run/emulator-acceleration.html#vm-mac)；

- 启动 Android Studio>Tools>Android>AVD Manager 并选择 `Create Virtual Device`；

- 选择一个设备并选择 Next；

- 为要模拟的Android版本选择一个或多个系统映像，然后选择 Next. 建议使用 x86 或 x86_64 的镜像；

- 在 Emulated Performance下, 选择 Hardware - GLES 2.0 以启用硬件加速；

- 验证AVD配置是否正确，然后选择 Finish；

  如果对以上步骤还有不清楚的可以参阅Android官方的 [Managing AVDs](https://developer.android.com/studio/run/managing-avds.html)文档。

  > 大家在安装过程中遇到问题无法解决的，可以在我们课程的[问答区提问](https://coding.imooc.com/learn/qa/321.html)进行[提问](https://coding.imooc.com/learn/qa/321.html)；

- 在 Android Virtual Device Manager中, 点击工具栏的 `Run`，模拟器启动并显示所选操作系统版本或设备的启动画面；
- 通过`flutter run`运行启动项目；

#### 如何在Android真机运行？

要准备在Android设备上运行并测试您的Flutter应用，您需要安装Android 4.1（API level 16）或更高版本的Android设备

- 在你的设备上启用 `开发人员选项` 和 `USB调试` 。详细说明可在[Android文档](https://developer.android.com/studio/debug/dev-options.html)中找到；
- 使用USB将手机插入电脑，如果有授权提示需要同意授权；
- 在终端中，运行`flutter devices` 命令以验证Flutter是否识别你连接的Android设备；
- 通过`flutter run`运行启动项目；

默认情况下，Flutter使用的Android SDK版本是基于你的 `adb` 工具版本， 如果你想让Flutter使用不同版本的Android SDK，则必须将该 `ANDROID_HOME` 环境变量修改SDK的目录。

#### 创建和运行一个简单的Flutter项目

**1.通过如下命令创建一个Flutter项目**

```bash
$ flutter create my_app  
```

**2.命令运行完成之后会在当前目录下创建一个名为`my_app`的Flutter项目，然后通过一下命令可以运行它：**

```bash
$ cd my_app  
$ flutter run  
```

## 在Mac上搭建Flutter开发环境

考虑到有不少小伙伴在用Mac系统做开发，那么在Mac该如何搭建Flutter开发环境呢？

- 系统要求
- 设置FLutter镜像(非必须)
- 获取Flutter SDK
- iOS开发环境设置
- Android开发环境设置
- 安装Flutter插件

### 系统要求

在Mac上要安装并运行Flutter要满足以下最低要求:

- 操作系统: macOS (64-bit)
- 磁盘空间: 2.8 GB (不包括IDE/tools的磁盘空间）.
- 工具: Flutter 依赖下面这些命令行工具：`bash curl git 2.x mkdir rm unzip which zip`

### 设置Flutter镜像(非必须)

由于在国内访问Flutter可能会受到限制，Flutter官方为中国开发者搭建了临时镜像，大家可以将如下环境变量加入到用户环境变量中：

```bash
//Macintosh HD⁩ ▸ ⁨Users⁩ ▸ ⁨你的用户名 ▸ ⁨.bash_profile  
export PUB_HOSTED_URL=https://pub.flutter-io.cn  
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn  
```

注意：此镜像为临时镜像，并不能保证一直可用，大家可以从 [Using Flutter in China](https://flutter.dev/community/china) 上获得有关镜像服务器的最新动态。

### 获取Flutter SDK

**1.点[Flutter官网](https://flutter.dev/docs/development/tools/sdk/archive)下载其最新可用的安装包。**

**2.解压安装包到你想安装的目录，如：**

```bash
$ cd ~/development  
$ unzip ~/Downloads/flutter_macos_1.17.3-stable.zip  
```

**3.添加flutter相关工具到path中：**

```bash
 export PATH="$PATH:`pwd`/flutter/bin"  
```

此代码只能暂时针对当前命令行窗口设置PATH环境变量，要想永久将Flutter添加到PATH中请参考下面做法：

```bash
$ cd ~  
$ vim .bash_profile  
```

然后添加：

```bash
export PATH=/Users/你的用户名/Documents/flutter/bin:$PATH  
```

之后记得保存文件。

#### 运行 flutter doctor

上面path配置完成之后，需要关闭终端重新打开，然后运行：

```bash
$ flutter doctor  
```

该命令检查你的环境并在终端窗口中显示报告。Dart SDK已经在捆绑在Flutter里了，没有必要单独安装Dart。 仔细检查命令行输出以获取可能需要安装的其他软件或进一步需要执行的任务（以粗体显示）：

例如：

```
[-] Android toolchain - develop for Android devices  
    • Android SDK at /Users/obiwan/Library/Android/sdk  
    ✗ Android SDK is missing command line tools; download from https://goo.gl/XxQghQ  
    • Try re-installing or updating your Android SDK,  
      visit https://flutter.dev/setup/#android-setup for detailed instructions.  
```

一般的错误会是XCode或Android Studio版本太低、或者没有`ANDROID_HOME`环境变量等，可参考一下环境变量的配置来检查你的环境变量：

```bash
//Macintosh HD⁩ ▸ ⁨Users⁩ ▸ ⁨你的用户名 ▸ ⁨.bash_profile  
#Android 环境变量  
export ANDROID_HOME=/Users/你的用户名/Library/Android/sdk  
#Android 模拟器路径  
export PATH=${PATH}:${ANDROID_HOME}/emulator  
#Android tools 路径  
export PATH=${PATH}:${ANDROID_HOME}/tools  
#Android 平台工具路径  
export PATH=${PATH}:${ANDROID_HOME}/platform-tools  
#Android NDK路径  
ANDROID_NDK_HOME=/Users/你的用户名/Library/Android/ndk/android-ndk-r10e  
#FLutter镜像  
export PUB_HOSTED_URL=https://pub.flutter-io.cn  
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn  
#Flutter环境变量  
export PATH=/Users/你的用户名/Documents/flutter/bin:$PATH  
```

> 第一次运行一个flutter命令（如flutter doctor）时，它会下载它自己的依赖项并自行编译。以后再运行就会快得多。

### iOS开发环境设置

#### 安装 Xcode

要用Flutter开发iOS App需要Xcode 9.0 或更高版本:

**1.安装Xcode 9.0或更新版本(通过[链接下载](https://developer.apple.com/xcode/)或[苹果应用商店](https://itunes.apple.com/us/app/xcode/id497799835))**

**2.配置Xcode命令行工具以使用新安装的Xcode版本** s

```
$ sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer  
```

以上路径时对于最新版Xcode的路径。如果你需要使用不同的Xcode版本，需要指定相应路径。

**3.确保Xcode许可协议是通过打开一次Xcode或通过命令sudo xcodebuild -license同意过了**

接下来就可以使用Xcode，在iOS设备或模拟器上运行Flutter App了。

#### 设置iOS模拟器

要准备在iOS模拟器上运行并测试您的Flutter应用，请按以下步骤操作：

**1.在终端输入如下命令打开一个iOS模拟器：**

```
$ open -a Simulator  
```

**2.通过模拟器菜单栏的 `硬件>设备` ，确保你打开是64位 iPhone 5s或更新的模拟器**

**3.如果模拟器过大，可以通过模拟器的 Window> Scale 菜单下设置设备比例**

#### 创建和运行一个简单的Flutter项目

**1.通过如下命令创建一个Flutter项目**

```bash
$ flutter create my_app  
```

**2.命令运行完成之后会在当前目录下创建一个名为`my_app`的Flutter项目，然后通过一下命令可以运行它：**

```bash
$ cd my_app  
$ flutter run  
```

## FAQ

### 无法启动模拟器

```
emulator: ERROR: x86 emulation currently requires hardware acceleration! Please  
ensure Windows Hypervisor Platform (WHPX) is properly installed and usable.  
CPU acceleration status: HAXM is not installed on this machine  
```

> 解决方案：选择 Tools > SDK Manager > SDK Tools , 安装 HAXM 即可

![android-emulator-acceleration](https://img3.sycdn.imooc.com/5ffaedb70001abae16281168.jpg)

### flutter no devices loading

#### 问题描述

在Android Studio上明明启动了模拟器但是还是提示 no devices，并且显示loading

#### 解决办法

重启Android Studio

### 新发布的包下载不下来

点击packages get 一直提示：

```bash
pub get failed (69) -- attempting retry  
```

#### 解决办法

在`.bash_profile`中取消pub的镜像：

```bash
#export PUB_HOSTED_URL=https://pub.flutter-io.cn  
#export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn  
```

### Android Studio创建Flutter项目卡死

#### 原因分析

网络原因是导致卡死的真凶，因为Android Studio创建Flutter项目需要联网下载一些国外服务器上的依赖包。

#### 解决办法

方案一：改为通过命令行的方式创建，亲测可行：

```bash
//创建一个名为flutter_ui的flutter项目  
flutter create flutter_ui  
//如果你想自定义包名可以通过如下方式进行  
flutter create --org org.dev.io.flutter.ui flutter_ui  
```

方案二：

- 关闭模拟器之后重试；
- 重启电脑后重试。

### Waiting for another flutter command to release the startup lock…

#### 解决办法

将文件

```
⁨flutter⁩ ▸ ⁨bin⁩ ▸ ⁨cache⁩ ⁩▸ lockfile  
```

删除即可。

## 参考

- [Flutter从入门到进阶 实战携程网App](https://coding.imooc.com/class/321.html)
- [移动端架构师](https://class.imooc.com/sale/mobilearchitect)