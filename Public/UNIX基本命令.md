

# UNIX基本命令



[详细在线文档 https://www.w3cschool.cn/unix/t6ve1pd1.html](https://www.w3cschool.cn/unix/t6ve1pd1.html)

# UNIX基本命令

* Mac系统采用的是UNIX文件系统,所有的文件都放在根目录/下面,因此没有Windows中分C盘、D盘 的概念
* 因为Mac系统是基于UNIX系统的,因此可以在“终端”中输入一些UNIX指令来操作Mac系统 常用的UNIX指令:\(需要经常使用才不容易忘记\)

```
ls :列出当前目录下的所有内容(文件\文件夹) 
pwd :显示出当前目录的名称
cd 文件夹 :进入所选文件夹
open 文件夹名称 ：打开文件夹 
cd ../ :返回上一级 
who :显示当前用户名
clear :清除所有内容
mkdir : 创建一个新目录
rm: 删除文件
rm -r: 删除文件夹 -f 强制删除
touch 文件名称: 创建文件
vi /open:打开、创建文件
-q 退出
-wq 保存并退出
-q!强制退出
i 进入编辑模式
esc 退出编辑模式
:wq!
cat/more 都可以查看文件内容
```

### 1. 必学命令

```
help [子命令] : 查看某一个具体的子命令的使用方法
```

### 2. 常用命令

```
- cd path : 将当前路径切换到path路径
- pwd ：查看当前所在路径
- ls (-a / -l / -G) :  查看当前文件夹下所有文件及文件夹
- touch filename1 filename2 ： 创建一个或者多个文件 
- rm filename : 删除文件
- open filename ：打开文件
- cat filename ：查看文件内容
- more filename ：分页查看文件内容
- mkdir 文件夹名称 ：创建一个文件夹
- mv oldFilePath newFilePath ：移动文件(可借助此命令给文件重命名)
```

### 3. 补充

```
.  代表当前文件路径
.. 代表上级目录

以 .开头的文件,代表隐藏文件
    * 显示隐藏文件
         defaults write com.apple.finder AppleShowAllFiles Yes && killall Finder
    * 不显示隐藏文件
        defaults write com.apple.finder AppleShowAllFiles No && killall Finder
```

### 4. 使用注意

```
1>  命令和参数之间需要添加空格
2>  如果要使用当前目录中的文件名，输入到一半时，按TAB键能够补全
```



