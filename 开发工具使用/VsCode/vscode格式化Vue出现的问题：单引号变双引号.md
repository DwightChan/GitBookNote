[toc]

<hr />

# vscode格式化Vue出现的问题：单引号变双引号

## 问题描述

在使用vscode格式化vue代码时，出现单引号变成了双引号问题（导致和EsLint要求不一致）：



![img](https:////upload-images.jianshu.io/upload_images/6169789-dd3a4fb92b903feb.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

## 解决方案

在项目根目录下新建文件：.prettierrc.json
 内容：



```json
{
    "singleQuote":true,
    "semi":false
}
```

## 附录

参考资料：https://www.cnblogs.com/nxmin/p/8523832.html

<hr />

作者：程序园中猿
链接：https://www.jianshu.com/p/ade598262e2d
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。