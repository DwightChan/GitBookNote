# cocopods遇到The dependency `XXXXXX` is not used in any concrete target的报错处理

```objc
The dependency `` is not used in any concrete target
The dependency `AFNetworking ` is not used in any concrete target


CocoaPods再遇困难，开发工具装了最新的，当我用CocoaPods的时候，出了一个提示，大概就是我的版本不是 last version，
然后给你提示了一个命令，直接复制即可，就是下面这个：


sudo gem install cocoapods --pre  //这里也可以先不用，先改一下podfile里面的格式，如下所示，不行再运行这里

安装cocoapods的预览版本，就会更新下来新的1.0.1.beta.2版本，如下所示：

Successfully installed cocoapods-1.0.0.beta.2
Parsing documentation for cocoapods-1.0.0.beta.2

很高兴啊，更新了新的版本，然而pod install就出错了，悲了个剧！出错如下：

Updating local specs repositories
Analyzing dependencies
[!] The dependency `FMDB (~> 2.3)` is not used in any concrete target.
The dependency `SDWebImage (~> 3.6)` is not used in any concrete target.
The dependency `AFNetworking (~> 2.3.0)` is not used in any concrete target.
The dependency `DACircularProgress (~> 2.2.0)` is not used in any concrete target.
The dependency `MBProgressHUD (~> 0.8)` is not used in any concrete target.
The dependency `PSTCollectionView (~> 1.2.1)` is not used in any concrete target.
The dependency `HPGrowingTextView (~> 1.1)` is not used in any concrete target.
The dependency `ProtocolBuffers (= 1.9.3)` is not used in any concrete target.
The dependency `leveldb-library (~> 1.18.1)` is not used in any concrete target.
The dependency `SCLAlertView-Objective-C (~> 0.7.5)` is not used in any concrete target.
The dependency `MWPhotoBrowser (~> 1.4.1)` is not used in any concrete target.
The dependency `MMMarkdown (~> 0.5)` is not used in any concrete target.
The dependency `MJExtension (~> 2.5.16)` is not used in any concrete target.
The dependency `MJRefresh (~> 2.4.12)` is not used in any concrete target.
The dependency `Masonry (~> 0.6.3)` is not used in any concrete target.


我用的三方库比较多，挺长的，出这个错是告诉我们我们所用的库没有指定target，它不知道用在哪里，所以就给报错了，然后我去了cocoapods的官网看了下，cocoapods官网地址https://cocoapods.org/

官网是这样给推荐的：
在创建Podfile的时候，用这种格式使用，

platform :iOS, '8.0'
#use_frameworks!个别需要用到它，比如reactiveCocoa

target 'MyApp' do
pod 'AFNetworking', '~> 2.6'
pod 'ORStackView', '~> 3.0'
pod 'SwiftyJSON', '~> 2.3'
end

然后终端  $ pod install  运行就可以了
里面的 MyApp 记得替换为自己攻城里面的target。这样就基本OK了，执行pod install / pod update 就都可以了。（use_frameworks! 这个是个别需要的，这里修改一下，可以把我上面的代码中的这一行【删除】）

下面是另外一种写法，

platform :ios, '8.0'
#use_frameworks!个别需要用到它，比如reactiveCocoa

def pods
pod 'AFNetworking', '~> 2.6'
pod 'ORStackView', '~> 3.0'
pod 'SwiftyJSON', '~> 2.3'
end
target 'MyApp' do
pods
end


如果不写版本号则都是以最新版,如下:  (注意: 大小写)

platform :ios, '8.0'

target 'MyApp' do
pod 'AFNetworking'
pod 'ORStackView'
pod 'SwiftyJSON'
end


```


[转载于:http://blog.csdn.net/zhaojinqiang12/article/details/51682191](http://blog.csdn.net/zhaojinqiang12/article/details/51682191)