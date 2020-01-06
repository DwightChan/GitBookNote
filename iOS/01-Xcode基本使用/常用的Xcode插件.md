# 常用的Xcode插件

- **Xcode插件大全**   
     <http://www.cocoachina.com/industry/20130918/7022.html>


- **必备**
- **文档注释生成：**<https://github.com/onevcat/VVDocumenter-Xcode>
- **自动检索图片名：**<https://github.com/ksuther/KSImageNamed-Xcode>
- **插件管理工具：**<https://github.com/mneorr/Alcatraz>

<br /><br />

- **移除插件**（可以使用上面提到的插件管理工具Alcatraz）   
到  /Users/当前用户名/Library/Application Support/Developer/Shared/Xcode/Plug-ins文件夹中删除


- **插件失效修复：**<http://joeshang.github.io/2015/04/10/fix-xcode-upgrade-plugin-invalid/>

---
<br/>

##使用Alcatraz来管理Xcode插件

- **使用Alcatraz来管理Xcode插件**

- **安装和删除**

  - **使用如下的命令行来安装Alcatraz：**

  ```
  mkdir -p ~/Library/Application\ Support/Developer/Shared/Xcode/Plug-ins;
  curl -L http://git.io/lOQWeA | tar xvz -C ~/Library/Application\ Support/Developer/Shared/Xcode/Plug-ins
  ```

  - **如果你不想使用Alcatraz了，可以使用如下命令来删除：**

  ```
  rm -rf ~/Library/Application\ Support/Developer/Shared/Xcode/Plug-ins/Alcatraz.xcplugin
  rm -rf ~/Library/Application\ Support/Alcatraz
  ```