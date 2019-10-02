# \#include指令
##本小节知识点:
1. 【了解】include基本概念
2. 【掌握】文件包含的格式
3. 【了解】#include <>和#include ""的区别

---

##1.include基本概念
- \#include 是C语言的预处理指令之一，所谓预处理，就是在编译之前做的处理，预处理指令一般以 # 开头

- \#include 指令后面会跟着一个文件名，预处理器发现 #include 指令后，就会根据文件名去查找文件，并把这个文件的内容包含到当前文件中。被包含文件中的文本将替换源文件中的 #include 指令，就像你把被包含文件中的全部内容拷贝到这个 #include 指令所在的位置一样。所以第一行指令的作用是将stdio.h文件里面的所有内容拷贝到第一行中。

- 如果被包含的文件拓展名为.h，我们称之为"头文件"(Header File)，头文件可以用来声明函数，要想使用这些函数，就必须先用 #include 指令包含函数所在的头文件

- \#include 指令不仅仅限于.h头文件，可以包含任何编译器能识别的C/C++代码文件，包括.c、.hpp、.cpp等，甚至.txt、.abc等等都可以

---
##2.文件包含的格式
当包含我们自己写的文件就是使用 #include "" 当包含系统􏰀供头文件的时候,就是用#include <>

- 示例:
```c
如:
#include <stdio.h>
#include <math.h>
#include "one.h"
```

- 注意:include 语句之后不需要加";"(因为#include它使一个预处理指令,不是一个语句)

---


##2.#include <>和#include ""的区别
- 二者的区别在于：当被include的文件路径不是绝对路径的时候，有不同的搜索顺序。
-  对于使用双引号""来include文件，搜索的时候按以下顺序：
    + 先在这条include指令的父文件所在文件夹内搜索，所谓的父文件，就是这条include指令所在的文件
    + 如果上一步找不到，则在父文件的父文件所在文件夹内搜索；
    + 如果上一步找不到，则在编译器设置的include路径内搜索；
    + 如果上一步找不到，则在系统的include环境变量内搜索

-  对于使用尖括号<>来include文件，搜索的时候按以下顺序：
    + 在编译器设置的include路径内搜索；
    + 如果上一步找不到，则在系统的include环境变量内搜索

```c
如果你是自己安装clang编译器，clang设置include路径是（4.2是编译器版本）：
/usr/lib/clang/4.2/include

Xcode自带编译器, clang设置include路径是
/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.10.sdk/usr/include

Mac系统的include路径有：
/usr/include
/usr/local/include

如果没有这个目录,可参考如下:
打开终端输入:xcode-select --install
安装Command Line Tools之后就会出现
```
---

##3.include注意事项
- include 不一定非要写在第一行
```c
int main()
{
#include "b.h"
    return 0;
}
```
- include的时候,可以包含路径。
```c
#include "text/b.h"
int main()
{
    return 0;
}
```


