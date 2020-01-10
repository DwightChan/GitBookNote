[toc]

<hr/>
# vsCode格式化插件

**ESlint**：是用来统一**JavaScript**代码风格的工具，**不包含css、html等**。

## 背景

近来研究前端，然后一直在百度上找VScode格式化（ESlint）的插件，结果找了半天都不靠谱。目前没有一个可以格式化html、css、符合ESlint的js、vue的插件，所以自己东拼西凑加实践找到解决方法。

## 一、安装插件

## ![img](https://img2018.cnblogs.com/blog/1173315/201907/1173315-20190717102442392-815606889.png)

1）**ESlint：**javascript代码检测工具，可以配置每次保存时格式化js，但每次保存只格式化一点点，你得连续按住Ctrl+S好几次,才格式化好，自行体会~~
2）**vetur：**可以格式化html、标准css（有分号 、大括号的那种）、标准js（有分号 、双引号的那种）、vue文件，
**但是！**格式化的标准js文件不符合ESlint规范，会给你加上双引号、分号等，像这样

![img](https://upload-images.jianshu.io/upload_images/6879756-a7f531f9a2bdbb99.png)

3）**Prettier - Code formatter：**只关注格式化，并不具有eslint检查语法等能力，只关心格式化文件(最大长度、混合标签和空格、引用样式等)，包括JavaScript · Flow · TypeScript · CSS · SCSS · Less · JSX · Vue · GraphQL · JSON · Markdown
4）**Manta's Stylus Supremacy：** 格式化stylus的插件（不用就不装），因为vetur会把css格式化有分号 、大括号的那种，此插件会把css格式化成stylus风格，像这样

![img](https://upload-images.jianshu.io/upload_images/6879756-ffaf25cc495575ea.png)

## 二、配置settings.json信息

File->Preference->Settings【也可以快捷键 ctr + ,（window系统） 直接打开】

![img](https://img2018.cnblogs.com/blog/1173315/201907/1173315-20190717104256901-4276878.png)

现在看到的是界面配置模式，点击右上角的大括号（如下图），可以打开 settings.json 文件。

![img](https://img2018.cnblogs.com/blog/1173315/201907/1173315-20190717103934915-111308914.png)

粘贴以下代码，保存即可

 ![img](https://img2018.cnblogs.com/blog/1173315/201907/1173315-20190717103424526-1185614657.png)

把代码贡献一下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
{
    // vscode默认启用了根据文件类型自动设置tabsize的选项
    "editor.detectIndentation": false,
    // 重新设定tabsize
    "editor.tabSize": 4,
    // #值设置为true时，每次保存的时候自动格式化；值设置为false时，代码格式化请按shift+alt+F
    "editor.formatOnSave": false,
    // #每次保存的时候将代码按eslint格式进行修复
    "eslint.autoFixOnSave": true,
    // 添加 vue 支持
    "eslint.validate": [
        "javascript",
        "javascriptreact",
        {
            "language": "vue",
            "autoFix": true
        }
    ],
    //  #让prettier使用eslint的代码格式进行校验
    "prettier.eslintIntegration": true,
    //  #去掉代码结尾的分号
    "prettier.semi": false,
    //  #使用带引号替代双引号
    "prettier.singleQuote": true,
    "prettier.tabWidth": 4,
    //  #让函数(名)和后面的括号之间加个空格
    "javascript.format.insertSpaceBeforeFunctionParenthesis": true,
    // #这个按用户自身习惯选择
    "vetur.format.defaultFormatter.html": "js-beautify-html",
    // #让vue中的js按"prettier"格式进行格式化
    "vetur.format.defaultFormatter.js": "prettier",
    "vetur.format.defaultFormatterOptions": {
        "js-beautify-html": {
            // #vue组件中html代码格式化样式
            "wrap_attributes": "force-aligned", //也可以设置为“auto”，效果会不一样
            "wrap_line_length": 200,
            "end_with_newline": false,
            "semi": false,
            "singleQuote": true
        },
        "prettier": {
            "semi": false,
            "singleQuote": true
        }
    },
    "[jsonc]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    // 格式化stylus, 需安装Manta's Stylus Supremacy插件
    "stylusSupremacy.insertColons": false, // 是否插入冒号
    "stylusSupremacy.insertSemicolons": false, // 是否插入分号
    "stylusSupremacy.insertBraces": false, // 是否插入大括号
    "stylusSupremacy.insertNewLineAroundImports": false, // import之后是否换行
    "stylusSupremacy.insertNewLineAroundBlocks": false,
    "prettier.useTabs": true,
    "files.autoSave": "off",
    "explorer.confirmDelete": false,
    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[json]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "diffEditor.ignoreTrimWhitespace": false // 两个选择器中是否换行
}
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

从此直接 Ctrl+S 就能一键格式化了。
