[toc]

<hr />
# VSCode下Vue代码自动格式化配置



本人是一名C++程序员，最近因为工作的原因需要使用Electron开发一个小软件，所以从未使用过前端技术的我需要快速学习HTML、CSS、ES6、Node.js、VUE等一大堆东西，开发环境也从常用的Visual Studio 2010\2015切换到了Visual Studio Code。不得不说VSCode很优秀，但确实不熟悉，经过大量的猜测及实践，我将过程整理如下：

## 1. 通过`electron-vue`创建工程

	选择安装`eslint`并选择`standard`风格，这就意味着只要代码不符合此风格，连运行都够呛，但代码风格统一是一名强迫症程序员的必备素质。
## 2. 语法高亮问题

	通过VSCode打开工程，所有的`*.vue`文件没有语法高亮，通过查询资料，安装`Vetur`插件后解决该问题，完美！

## 3. 安装`ESLint`插件

	为了能让`eslint`的配置生效，需要安装`ESLint`插件;
	安装完毕后，发现所有`*.js`文件里代码风格与`eslint`的`standard`风格不符的地方都以红色波浪线标识出来了，但是，`*.vue`文件里的js代码并没有，添加如下配置后解决该问题，完美！

```json
"eslint.validate": [
    "javascript",
    "javascriptreact",
    {
        "language": "vue",
        "autoFix": true
    }
]
```

## 4. 修改配置

1. 现在我们希望能在保存代码的时候自动格式化，只需加上`"editor.formatOnSave": true`这个配置就可以了，但是我们发现虽然保存时代码能够自动格式化，但是并不会修复与`eslint`的`standard`风格不符合的地方，别急，加上`"eslint.autoFixOnSave": true`这个配置即可解决该问题，完美！

2. 等等，貌似发现几个问题，在`*.vue`文件里，保存文件时，会发现js代码会先格式化成另外一种风格，然后再被`eslint`给修复，现象就是先出现大量红色波浪线，然后又消失，但是`*.js`文件里不会出现此现象，所以猜测是`Vetur`搞的鬼，经实践发现，只需加上`"vetur.format.defaultFormatter.js": "none"`即可解决该问题，完美！

3. 现在还剩最后一个问题，`*.vue`文件里的`html`代码在保存时并没有自动格式化，通过查询资料发现，只需加上`"vetur.format.defaultFormatter.html": "js-beautify-html"`配置即可解决该问题，完美！

4. 此时，代码格式化问题已全部解决，所有的配置如下：

```js
// 保存自动化
"editor.formatOnSave": true,
// 保存时自动fix
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
// 使用插件格式化 html
"vetur.format.defaultFormatter.html": "js-beautify-html",
// 屏蔽vetur的js格式化
"vetur.format.defaultFormatter.js": "none"
```

<hr />
作者：Mr.Victor
链接：https://juejin.im/post/5aeddf14f265da0b736d8a66
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。