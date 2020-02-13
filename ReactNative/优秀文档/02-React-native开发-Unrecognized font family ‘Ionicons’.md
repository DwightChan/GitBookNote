[toc]

---

# React-native开发-Unrecognized font family ‘Ionicons’

> > 原创zhaolaoda2012 最后发布于2018-09-11 16:18:17 阅读数 1688  收藏

错误如下：

![](https://img-blog.csdn.net/20180911160629351?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW9sYW9kYTIwMTI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

解决方法：
先打开你的react-native项目的ios文件夹下面的项目，右键选择add file

![](https://img-blog.csdn.net/20180911161339346?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW9sYW9kYTIwMTI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

将font文件添加到项目里面：

![](https://img-blog.csdn.net/20180911161425562?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW9sYW9kYTIwMTI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)


然后还需要到info.plist文件添加一些配置：

![](https://img-blog.csdn.net/20180911161503252?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW9sYW9kYTIwMTI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

复制下面的内容到plist里面:

```
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
如下图：

![](https://img-blog.csdn.net/20180911161618579?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW9sYW9kYTIwMTI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

这样就大功告成啦。重新运行项目就行了。
————————————————
版权声明：本文为CSDN博主「zhaolaoda2012」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/zhaolaoda2012/article/details/82627735