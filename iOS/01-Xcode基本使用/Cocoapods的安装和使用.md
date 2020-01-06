# Cocoapods的安装和使用

```objc
1.先升级Gem
    sudo gem update --system
2.切换cocoapods的数据源
    【先删除，再添加，查看】
    gem sources --remove https://rubygems.org/
    gem sources -a https://ruby.taobao.org/
    gem sources -l
3.安装cocoapods
    sudo gem install cocoapods
    或者（如10.11系统）sudo gem install -n /usr/local/bin cocoapods
4.将Podspec文件托管地址从github切换到国内的oschina（该步骤可以省略）
    【先删除，再添加，再更新】
    pod repo remove master
    pod repo add master http://git.oschina.net/akuandev/Specs.git
    pod repo add master https://gitcafe.com/akuandev/Specs.git
    pod repo update
5.设置pod仓库
    pod setup
6.测试
    【如果有版本号，则说明已经安装成功】
    pod --version
7.利用cocoapods来安装第三方框架
    01 进入要安装框架的项目的.xcodeproj同级文件夹
    02 在该文件夹中新建一个文件podfile
    03 在文件中告诉cocoapods需要安装的框架信息
        a.该框架支持的平台
        b.适用的iOS版本
        c.框架的名称
        d.框架的版本
8.安装
pod install --no-repo-update
pod update --no-repo-update

9.说明
platform :ios, '8.0' 用来设置所有第三方库所支持的iOS最低版本
pod 'SDWebImage','~>2.6' 设置框架的名称和版本号
版本号的规则：
'>1.0'    可以安装任何高于1.0的版本
'>=1.0'   可以安装任何高于或等于1.0的版本
'<1.0'    任何低于1.0的版本
'<=1.0'   任何低于或等于1.0的版本
'~>0.1'   任何高于或等于0.1的版本，但是不包含高于1.0的版本
'~>0'     任何版本，相当于不指定版本，默认采用最新版本号

10.使用pod install命令安装框架后的大致过程：
01 分析依赖:该步骤会分析Podfile,查看不同类库之间的依赖情况。如果有多个类库依赖于同一个类库，但是依赖于不同的版本，那么cocoaPods会自动设置一个兼容的版本。
02 下载依赖:根据分析依赖的结果，下载指定版本的类库到本地项目中。
03 生成Pods项目：创建一个Pods项目专门用来编译和管理第三方框架，CocoaPods会将所需的框架，库等内容添加到项目中，并且进行相应的配置。
04 整合Pods项目：将Pods和项目整合到一个工作空间中，并且设置文件链接。
```

---
<br/>