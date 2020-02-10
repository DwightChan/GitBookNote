[toc]

---

# React-native 高级坑 Invariant Violation:Application 项目名 has not been registered.



因为我的错误是基于这个描述之上的，但是中间有个很诡异的问题 ，请有问题的同学看完，我会在最后解答。
**前言**
**在学习一门新技术的你也许有跟我一样的困惑，照着书上或者视频上的敲了。但是就是有各种问题没有出来自己想要的结果。我会将自己在这个过程中遇到的坑都记录下来，不一定全覆盖，但希望这些文章可以解决你的问题。**

------

**错误提示**
Invariant Violation:Applicaction 项目名 has not been registered.This is either due to a require() error during initialization or failure to call AppRegistry.registerCommponent.
[[图片上传中。。。（1）\]](https://www.jianshu.com/u/a2710bc5209a) 作者 [李将军杀到](https://www.jianshu.com/u/a2710bc5209a) **关注2016.01.10 12:14 字数 347 阅读 3698评论 10喜欢 12

**前言**
**在学习一门新技术的你也许有跟我一样的困惑，照着书上或者视频上的敲了。但是就是有各种问题没有出来自己想要的结果。我会将自己在这个过程中遇到的坑都记录下来，不一定全覆盖，但希望这些文章可以解决你的问题。**

------

**错误提示**
Invariant Violation:Applicaction 项目名 has not been registered.This is either due to a require() error during initialization or failure to call AppRegistry.registerCommponent.
这个错误的根本原因是根目录./index.ios.js中

AppRegistry.registerComponent('项目名',() => ...);
与./ios/项目名/appDelegate.m中的

RCTRootView*rootView = [[RCTRootViewalloc]initWithBundleURL:jsCodeLocation

moduleName:@"项目名" launchOptions:launchOptions];
或是./android/app/src/main/java/com/项目名/MainActivity.java中的

mReactRootView.startReactApplication(mReactInstanceManager, "项目名", null);
没有保持一致，解决方法很简单。编辑成相同的参数即可。

但是，还有一种情况！

即便你确保一致了但还是出现相同的错误提示，这又是怎么搞得呢？这个时候你可以检查一下你的命令行。有可能你同时在运行一个以上的程序，像我。如果你的react-native在运行程序A而你打开了程序B，也会出现相同的问题。**解决方法很简单，关掉命令行运行程序。ctrl+c,运行你想运行的程序。**

其实我遇到的问题很奇怪，明明每个步骤都没有错误，但是就是还是有问题。为什么会出问题，而且还不一样。那可能是需求也不一样吧。
我的需求是要从android 代码跳到React-native页面，所以大家都会用到

> ReactRootView.startReactApplication(mReactInstanceManager, moduleName, null);

这段代码是没有问题的，但是问题的在下面

> private ReactInstanceManager setDefaultReactConfig() {
> return ReactInstanceManager.builder()
> .setApplication(getApplication())
> .setBundleAssetName("index.android.bundle")
> .setJSMainModuleName("index.android")
> .addPackage(new MainReactPackage())
> //.addPackage(new VectorIconsPackage())
> .addPackage(new AppReactPackage())
> .setUseDeveloperSupport(false)
> .setInitialLifecycleState(LifecycleState.RESUMED)
> .build();
> }

看到没有， .setUseDeveloperSupport(false) 就是把调试模式关了，然后就没法和服务器通信了，所以你一直拿不到最新的服务器代码，然后就会一直报这个错误。



---

>作者 [李将军杀到](https://www.jianshu.com/u/a2710bc5209a) （为了节省时间，复制了一下这个作者的原贴，特此声明 ）
>原贴地址：[http://www.jianshu.com/p/82a09063e61c](https://www.jianshu.com/p/82a09063e61c)
