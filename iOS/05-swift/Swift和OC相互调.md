#Swift和OC相互调




---
> 在项目中不免会有多中语言开发, 不说别的就我个人而言, 之前一直都是用 OC 写的代码, 封装很多工具类, 而苹果新出来 Swift ,  现在项目在向 Swift 过渡, 或者新项目是 Swift , 暂时没有时间用 Swift 封装工具类,  但有想在 OC 中可以用 Swift 的代码, Swift 文件也可以用 OC 的代码, 此时我们只要通过响应的配置做好桥接即可在 Swift 和 OC 中相互使用对方的资源!!!

>下面我就给大家分享 Swift 与 OC 相互调用的配置以及注意点!!!

>建议收藏!!!


###1. Swift 调用 OC

- 创建桥接文件件—>`xxxx.h`
- 在桥接文件中导入OC代码头文件
- 配置桥接文件: 项目 ->buildSettings —> bridging —> 配置

![创建桥接文件.png](http://img.blog.csdn.net/20160804224421899)

![配置桥接文件.png](http://img.blog.csdn.net/20160804224516503)

![桥接文件相对路径.png](http://img.blog.csdn.net/20160805185805004)

![在桥接文件中导入 OC 类头文件.png](http://img.blog.csdn.net/20160805185856172)

![在 Swift 文件中使用 OC 类.png](http://img.blog.csdn.net/20160805185925001)


---
###2. OC 调用 Swift
- 项目名字不能随便起: 
    - 不能有特殊符号(`@ # $ % ^ ~ ! ? < > & - _ + , . " ' | \ { ( ) }`)
    - 也不能有中文
    - 最好纯英文(和数字), 以英文字母开头
- Swift中的类/属性/法必须使 public修饰 
- 导入 项目名称-Swift.h

![Swift中的类/属性/法必须使 public修饰.png](http://img.blog.csdn.net/20160805190004614)

![OC项目调用 Swift 文件.png](http://img.blog.csdn.net/20160805190049552)


---