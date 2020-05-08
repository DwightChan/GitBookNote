[toc]

---

# code-push常用命令

[_九卿_](https://www.jianshu.com/u/59ca70f08bf3)关注

12018.04.10 17:41:16字数 796阅读 13,337

[React-Native Android集成Code-Push 热更新：demo](https://www.jianshu.com/p/725624989dfe)

###### 1. code-push常用命令

- 安装: npm install -g code-push-cli
- 注册账号: code-push register
- 登陆: code-push login
- 注销: code-push logout
- 添加项目: code-push app add <appName> <os> <platform>
- 删除项目: code-push app remove <appName> <os> <platform>
- 列出账号下的所有项目: code-push app list
- 显示登陆的token: code-push access-key ls
- 删除某个access-key: code-push access-key rm <accessKey>
- 添加协作人员：code-push collaborator add <appName> [next@126.com](mailto:next@126.com)
- 部署一个环境: code-push deployment add <appName> <deploymentName>
- 删除部署: code-push deployment rm <appName>
- 列出应用的部署: code-push deployment ls <appName>
- 查询部署环境的key: code-push deployment ls <appName> -k
- 查看部署的历史版本信息: code-push deployment history <appName> <deploymentNmae>
- 重命名一个部署: code-push deployment rename <appName> <currentDeploymentName> <newDeploymentName>

###### 2. 集成到项目

1. 在项目目录下, 安装CodePush插件



```java
npm install --save react-native-code-push
```

1. 引入到Xcode工程, 有两种方法, 第一种手动加入, 第二种使用rnpm自动引入, 第三种使用cocoaPods接入:

- 第二种:



```undefined
安装rnpm: npm -g install rnpm xcode
使用rnpm: rnpm link
```

- 第三种:



```jsx
修改Podfile文件：(注意路径正确): 
pod 'CodePush', :path => './node_modules/react-native-code-push'

执行命令行更新pod：
pod install 或者 pod install --verbose --no-repo-update
```

1. 在Xcode里AppDelegate.m里 修改



```cpp
//  jsCodeLocation = [[RCTBundleURLProvider sharedSettings] jsBundleURLForBundleRoot:@"index.ios" fallbackResource:nil];
#ifdef DEBUG
  jsCodeLocation = [[RCTBundleURLProvider sharedSettings] jsBundleURLForBundleRoot:@"index.ios" fallbackResource:nil];
#else
  jsCodeLocation = [CodePush bundleURL];
#endif
```

1. 修改info.plist 添加CodePushDeploymentKey键值对中的Staging的值，Deployment Key可以通过命令code-push deployment ls appName --displayKeys进行获取.也可以使用$(CODEPUSH_KEY)来自动适配Production或Staging环境, 如果填的是Production的key, 则打的包就是Production的包, 如果填的是Staging的key, 则打的包就是Staging的包.
2. 修改info.plist 中 Bundle versions string, short的值改成三位数字,如1.0.0, 不然会报错

###### 3. 发布更新

- 自动打包发布
  自动打包你的js和资源文件成bundle并且上传发布到CodePush的服务器(注意: 默认是Staging环境):



```bash
code-push release-react MyApp ios --plistFile ../MyApp/Info.plist -t "1.0.0" --des "测试完毕还原原状" -m true -d development
```

- 手动打包发布
  自己打包有两种: 第一种只是更新js文件(可整个项目的js文件/当个js文件), 第二种js文件+images文件(release 整个文件夹)

第一种单单js文件:



```go
1. 创建一个bundles文件夹
打包命令: 
// react-native bundle --platform 平台 --entry-file 启动文件 --bundle-output 打包js输出文件 --assets-dest 资源输出目录 --dev 是否调试 
打包整个项目的js文件: 
react-native bundle --platform ios --entry-file index.ios.js --bundle-output ./bundles/main.bundle --dev false

2. 发布更新
发布命令: 
// code-push release <应用名称> <Bundles所在目录> <对应的应用版本> --deploymentName 更新环境 --description 更新描述 --mandatory 是否强制更新
例如:
code-push release HybridDemo ./bundles/main.bundle 1.0.0 --deploymentName Production --description "第四次更新" --mandatory true

测试版的发布不能搞到正式版，promote命令 目前理解就是把测试环境copy到正式环境
```

第二种js文件+图片资源:



```java
// 1. –assets-dest 后就是放图片的文件夹路径
react-native bundle --platform ios --entry-file index.ios.js --bundle-output ./bundles/qqm.jsbundle --assets-dest ./bundles --dev false

// 2. push bundles文件
code-push <release/debug> <projectName(与注册的app同名)><bundle文件名> <版本号>
例如: 
code-push release appName ./bundles 1.0.0
```

- 更新规则



```undefined
你APP内plist文件写的版本号可能是1.0.0，所以你的reactjs打包上传的版本也要是1.0.0（而不是1.0.1这样递增），你需要和APP保持一致，然后服务器会根据你最新上传的且和APP一样的版本作为最新版。

范围表达式

* 1.2.3 仅仅只有1.2.3的版本

* *所有版本

* 1.2.x 主要版本1，次要版本2的任何修补程序版本

* 1.2.3 - 1.2.7 1.2.3版本到1.2.7版本

* >=1.2.3 <1.2.7 大于等于1.2.3版本小于1.2.7的版本

* ~1.2.3 大于等于1.2.3版本小于1.3.0的版本

* ^1.2.3 大于等于1.2.3版本小于2.0.0的版本
```

- 修改更新



```tsx
Usage: code-push patch <appName> <deploymentName> [--label <label>] [--description <description>] [--disabled] [--mandatory] [--rollout <rolloutPercentage>]

选项：
  --label, -l           指定标签版本更新，默认最新版本 [string] [默认值: null]
  --description, --des  描述  [string] [默认值: null]
  --disabled, -x        是否禁用该更新  [boolean] [默认值: null]
  --mandatory, -m       是否强制更新  [boolean] [默认值: null]
  --rollout, -r         此更新推送用户的百分比，此值仅可以从先前的值增加。  [string] [默认值: null]

示例：
  code-push patch MyApp Production --des "Updated description" -r 50         修改"MyApp"的"Production"部署中最新更新的描述 ，并且更新推送范围为50％
  code-push patch MyApp Production -l v3 --des "Updated description for v3"  修改"MyApp"的"Production"部署中标签为v3的更新的描述
```

- 升级环境



```tsx
Usage: code-push promote <appName> <sourceDeploymentName> <destDeploymentName> [--description <description>] [--mandatory] [--rollout <rolloutPercentage>]

选项：
  --description, --des  描述  [string] [默认值: null]
  --disabled, -x        是否禁用该更新  [boolean] [默认值: null]
  --mandatory, -m       是否强制更新  [boolean] [默认值: null]
  --rollout, -r         此促进更新推送用户的百分比  [string] [默认值: null]

示例：
  code-push promote MyApp Staging Production                                   "MyApp"中"Staging"部署的最新更新发布到"Production"部署中
  code-push promote MyApp Staging Production --des "Production rollout" -r 25  "MyApp"中"Staging"部署的最新更新发布到"Production"部署中, 并且只推送25%的用户
```

- 回滚更新



```csharp
Usage: code-push rollback <appName> <deploymentName> [--targetRelease <releaseLabel>]

选项：
  --targetRelease, -r  指定回归到哪个标签，默认是回滚到上一个更新  [string] [默认值: null]

示例：
  code-push rollback MyApp Production                     "MyApp"中"Production"部署执行回滚
  code-push rollback MyApp Production --targetRelease v4  "MyApp"中"Production"部署执行回滚，回滚到v4这个标签版本
```



```css
当部署的版本不同时，不能跨版本回滚。
例如：CodePush历史版本中为2.10.1，此时发布2.10.2版本。
当从2.10.2发起回滚操作回到2.10.1时，是不可行的。
```

- js内写法



```dart
如果有发布热更新时 mandatory 则 Code Push 会根据 mandatory 是 true 或false 来控制应用是否强制更新。默认情况下 mandatory 为 false 即不强制更新。mandatory 为 false时以下三种设置方法才有效

// 第一种:
codePush.sync();

// 第二种:
codePush.sync({
    updateDialog: false,
    installMode: codePush.InstallMode.IMMEDIATE
});

// 第三种:
CodePush.sync({
    deploymentKey: 'deployment-key-here',
    updateDialog: {
        optionalIgnoreButtonLabel: '稍后',
        optionalInstallButtonLabel: '后台更新',
        optionalUpdateMessage: '有新版本了，是否更新？',
        title: '更新提示'
    },
    installMode: CodePush.InstallMode.IMMEDIATE
});

三种更新的策略: 配置到installMode: 之后即可生效
* IMMEDIATE 立即更新APP
* ON_NEXT_RESTART 到下一次启动应用时
* ON_NEXT_RESUME 当应用从后台返回时
```

- 项目实际发布时使用命令

1. 登录: code-push login
2. 列出账号下的所有项目: code-push app list
3. 列出应用的部署: code-push deployment ls MyApp
4. 查看部署的历史版本信息: code-push deployment history MyApp Debug
5. 发布版本更新: code-push release-react MyApp ios -d Staging -p ../MyApp/Info.plist --des 'UI调整' -t '1.0.2'
6. 把更新推到另一个环境: code-push promote QQMProjec Staging Production
7. 关闭某个版本: code-push patch MyApp Staging -l v13 --des '关闭v13' -x true

注意：
在关联项目登录的时候，有时候已经登录其他账号，需要查看登录账号或者退出的话
进入reactnative 项目根目录执行命令查看当前是否登录，先保证没有别的账号正在登录



```undefined
code-push whoami
```

如果报错如下，表示没有登录



```jsx
[Error]  You are not currently logged in. Run the 'code-push login' command to authenticate with the CodePush server.
```

如果没有报错 且显示邮箱账号，则表示已经登录账户，我们要先注销当前账号



```bash
code-push logout
```

成功注销后执行登录指令，登录服务器



```cpp
code-push login http://localhost:8080
```



```cpp
参考文章：
https://segmentfault.com/a/1190000008591456
https://blog.csdn.net/zhuchuanwu2013/article/details/51262718
https://www.jianshu.com/p/51b36ed583ef
```



19人点赞



[React Native](https://www.jianshu.com/nb/23801375)