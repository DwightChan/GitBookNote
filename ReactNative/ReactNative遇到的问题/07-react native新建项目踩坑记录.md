[toc]



----



# [react native新建项目踩坑记录](https://segmentfault.com/a/1190000039281109)



### 问题一：

ios环境下按照官网步骤并且pod已经设置完清华源后启动`npm run ios`,报错如下：

```awk
** BUILD FAILED **


The following build commands failed:
    CompileC /Users/loser/Library/Developer/Xcode/DerivedData/test0205-dasunahpjpavelgmslwgmvjhesxy/Build/Intermediates.noindex/Pods.build/Debug-iphonesimulator/Flipper.build/Objects-normal/x86_64/FlipperRSocketResponder.o /Users/loser/Documents/projects/test0205/ios/Pods/Flipper/xplat/Flipper/FlipperRSocketResponder.cpp normal x86_64 c++ com.apple.compilers.llvm.clang.1_0.compiler
(1 failure)
```

### 解决方案

网上大部分的答案全都是类似这种:

```
1.  cd /ios
2.  run `pod install`
3.  cd ..
4.  delete _build_ folder
5.  run `react-native run-ios`
```

亲测无效。
正确的解决方案如下：
这是因为iOS项目`use_flipper`中的use_flipper。

```erlang-repl
use_flipper! 
```

因此，我需要使用use_flipper来指示`Flipper-Folly`版本为

```apache
use_flipper!({ 'Flipper-Folly' => '2.3.0' }) 
```

更改之后，它运行完美。

> 如果安装pod依赖过程中卡在`boost-for-react-native`或其他依赖，请在ios/Podfile文件头加入`pod 'boost-for-react-native', :git => 'https://gitee.com/mirrors/boost-for-react-native.git’`，下载gitee中的依赖，另外，控制台需要单独配置代理，你的梯子默认是不对控制台生效的

### 问题二：

解决以上问题后运行，再次报错，如下：

```subunit
error: Can’t find ‘node’ binary to build React Native bundle If you have non-standard nodejs installation, select your project in Xcode, find ‘Build Phases’ - ‘Bundle React Native code and images’ and change NODE_BINARY to absolute path to your node executable (you can find it by invoking ‘which node’ in the terminal)
```

因为我是使用了nvm作为node的版本管理工具，所以xCode在使用node时，找不到。

```bash
which node
/Users/sharkship/.nvm/versions/node/v12.16.1/bin/node
```

我们可以使用软连接的方式，将node链接到 `/usr/local/bin/node`目录上，xCode即可找到node

```bash
ln -s $(which node) /usr/local/bin/node
```

当然在使用`nvm`更换完node版本时，需要使用上述命令进行node的更新。

### 问题四：

Native应用中的PhaseScriptExecution错误，具体报错信息如下：

```vhdl
error Failed to build iOS project. We ran "xcodebuild" command but it exited with error code 65. To debug build logs further, consider building your app with Xcode.app, by opening BoltAssignment.xcworkspace.
Command line invocation:
    /Applications/Xcode.app/Contents/Developer/usr/bin/xcodebuild -workspace BoltAssignment.xcworkspace -configuration Debug -scheme BoltAssignment -destination id=3E598855-6D4F-4F36-BEE1-8663A1F71787


nvm is not compatible with the "PREFIX" environment variable: currently set to "/usr/local"
Run `unset PREFIX` to unset it.
nvm is not compatible with the "PREFIX" environment variable: currently set to "/usr/local"
Run `unset PREFIX` to unset it.
Command PhaseScriptExecution failed with a nonzero exit code

warning: The iOS Simulator deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 8.0, but the range of supported deployment target versions is 9.0 to 14.4.99. (in target 'Flipper-Glog' from project 'Pods')
warning: The iOS Simulator deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 8.4, but the range of supported deployment target versions is 9.0 to 14.4.99. (in target 'Flipper-PeerTalk' from project 'Pods')
warning: The iOS Simulator deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 8.0, but the range of supported deployment target versions is 9.0 to 14.4.99. (in target 'libwebp' from project 'Pods')
warning: The iOS Simulator deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 8.0, but the range of supported deployment target versions is 9.0 to 14.4.99. (in target 'YogaKit' from project 'Pods')
warning: Capabilities for Signing & Capabilities may not function correctly because its entitlements use a placeholder team ID. To resolve this, select a development team in the BoltAssignment editor. (in target 'BoltAssignment' from project 'BoltAssignment')
warning: The iOS Simulator deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 8.0, but the range of supported deployment target versions is 9.0 to 14.4.99. (in target 'Flipper-DoubleConversion' from project 'Pods')
warning: The iOS Simulator deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 8.0, but the range of supported deployment target versions is 9.0 to 14.4.99. (in target 'boost-for-react-native' from project 'Pods')
warning: no rule to process file '/Users/harsh_nagalla/dev/BoltAssignment/ios/Pods/Flipper-RSocket/rsocket/README.md' of type 'net.daringfireball.markdown' for architecture 'x86_64' (in target 'Flipper-RSocket' from project 'Pods')
warning: no rule to process file '/Users/harsh_nagalla/dev/BoltAssignment/ios/Pods/Flipper-RSocket/rsocket/benchmarks/CMakeLists.txt' of type 'text' for architecture 'x86_64' (in target 'Flipper-RSocket' from project 'Pods')
warning: no rule to process file '/Users/harsh_nagalla/dev/BoltAssignment/ios/Pods/Flipper-RSocket/rsocket/benchmarks/README.md' of type 'net.daringfireball.markdown' for architecture 'x86_64' (in target 'Flipper-RSocket' from project 'Pods')
warning: The iOS Simulator deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 8.0, but the range of supported deployment target versions is 9.0 to 14.4.99. (in target 'RNFastImage' from project 'Pods')
warning: The iOS Simulator deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 8.0, but the range of supported deployment target versions is 9.0 to 14.4.99. (in target 'SDWebImageWebPCoder' from project 'Pods')

** BUILD FAILED **


The following build commands failed:
    PhaseScriptExecution [CP-User] Generate Specs /Users/harsh_nagalla/Library/Developer/Xcode/DerivedData/BoltAssignment-cxeqsscopunscndrzxcrfnugkasb/Build/Intermediates.noindex/Pods.build/Debug-iphonesimulator/FBReactNativeSpec.build/Script-1F0D93C9412E4439D9C46216EB143B15.sh
(1 failure) 
```

出现这个问题的场景是我按照官方文档新建了一个项目，没有出现上述的问题，与之前操作不通的是，这次安装pod依赖我是用的`pod install --verbose --no-repo-update`。但是`yarn ios`尝试运行项目时就出现以上错误（**提醒：不要npm与yarn混用**）

解决方案：
`npx react-native run-ios`代替`yarn ios`解决了这个问题。

### 问题五：

```vim
Build system information
error: Multiple commands produce '/Users/mac/Library/Developer/Xcode/DerivedData/ReactNativeProject-erfowopvthnfaidafpmlevtdurad/Build/Products/Debug-iphonesimulator/ReactNativeProject.app/Entypo.ttf':
1) Target 'ReactNativeProject' (project 'ReactNativeProject') has copy command from '/Users/mac/study-demo/ReactNativeProject/node_modules/react-native-vector-icons/Fonts/Entypo.ttf' to '/Users/mac/Library/Developer/Xcode/DerivedData/ReactNativeProject-erfowopvthnfaidafpmlevtdurad/Build/Products/Debug-iphonesimulator/ReactNativeProject.app/Entypo.ttf'
2) That command depends on command in Target 'ReactNativeProject' (project 'ReactNativeProject'): script phase “[CP] Copy Pods Resources”
```

balabala一堆看到好几个`.ttf`的字眼，推测就是我自己引用的icon依赖（`react-native-vector-icons`）可能有问题，此项目我自定义安装的依赖有如下：

```less
@react-native-community/masked-view
@react-navigation/bottom-tabs
@react-navigation/native
@react-navigation/stack
react-native-gesture-handler
react-native-reanimated
react-native-safe-area-context
react-native-screens
react-native-swiper
react-native-vector-icons 
```

于是：
`react-native unlink react-native-vector-icons`,重新运行项目后正常，但是这样的话icon库肯定就是用不了了，后面需要另外找方案。

#### 解决字体库问题：

2021-4-11 22:15 更新说明一下引用`react-native-vector-icons`字体库报错的原因：
查阅了stackoverflow上这样一篇讨论：[https://stackoverflow.com/que...](https://link.segmentfault.com/?enc=GrQ7of3Q5l7g8q35ESc5%2BA%3D%3D.wj83rJ%2FW0DlqrHmI3HdLtViqoiFOI5pY%2FLwJ%2FAIqesfol9Bp0El0IoF%2B%2FzKOX0mE9E4JE1ir483myrpTa8WqdTd2ZRxLwmNyF9Ibf8CLuTvqW1R9ACtjpwiXsU8kHdmR51cT9JonJp0nVoHL6k99ejqqhwFca5ofnKy4GMgeolKMbLFG%2BLKkX3MQ0ubAkTkPZk5FPfZsdtu85%2FxKzrLBxyprn1nqe%2FSwRrm1nUEgz%2B9PeqGOWMP6T04d6zyX4BknqHMR4mfDGk7Xuik9C%2B5jCA%3D%3D)

Editing PodFile and adding pod `RNVectorIcons` not necessary because **auto-linking** will work fine after adding **react-native-vector-icons**

adding to PodFile will cause a warning after the next run with `react-native run-ios`:

```pgsql
Warning: following modules are linked manually: - react-native-vector-icons (to unlink run: "react-native unlink react-native-vector-icons" 
```

Just add this line of codes to your **info.plist** that exist on ios/yourPorjectName/

find **UIAppFonts** and add codes inside :

```xml
 <key>UIAppFonts</key>
 <array>
     <string>AntDesign.ttf</string>
     <string>Entypo.ttf</string>
     <string>EvilIcons.ttf</string>
     <string>Feather.ttf</string>
     <string>FontAwesome.ttf</string>
     <string>FontAwesome5_Brands.ttf</string>
     <string>FontAwesome5_Regular.ttf</string>
     <string>FontAwesome5_Solid.ttf</string>
     <string>Fontisto.ttf</string>
     <string>Foundation.ttf</string>
     <string>Ionicons.ttf</string>
     <string>MaterialCommunityIcons.ttf</string>
     <string>MaterialIcons.ttf</string>
     <string>Octicons.ttf</string>
     <string>SimpleLineIcons.ttf</string>
     <string>Zocial.ttf</string>
 </array>
```

不得不说编程上的坑，`stackoverflow`上百分之99都能找到答案。



### 其他解决办法

```
I struggled to build react native project in iOS with this issue. And I did build after following processes.

Clear the cache of pod with
rm -rf ~/Library/Caches/CocoaPods
rm -rf Pods
rm -rf ~/Library/Developer/Xcode/DerivedData/*
pod deintegrate
pod setup
And delete the project's Pods directory. The location of it is project directory > ios > Pods.
Then in the project directory > ios location, install pod with pod install
And react-native run-ios in project directory.
After I faced the issue, I try to build the project in another Mac and work fine. And I found the every error is from folly and it is in Pods. Then I compared Pods directory between mine and another Mac environment. In my case, there are missing files. So I reference the comment written by kelset in 'folly/folly-config.h' file not found, said "This happens when your pod cache is corrupted.". So I check the way of clearing cache of pod, and it works.

```



### 六 端口8081 被占用

直接使用其他端口 My port 8081 was blocked by McAfee. Using a different port directly wasn't working `react-native start --port=8082` and `react-native run-ios --port=8082`

[![enter image description here](https://i.stack.imgur.com/YmxER.jpg)](https://i.stack.imgur.com/YmxER.jpg)



