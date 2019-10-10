[TOC]

---

# 再学一次 gulp

原文链接：[https://juejin.im/entry/586a417561ff4b006d77fe85](https://juejin.im/entry/586a417561ff4b006d77fe85)

## 1. gulp
### 1.1 什么是gulp
> Gulp是可以自动化执行任务的工具。在平时开发的流程里面，一定有一些动作需要手工的重复的去执行，比如:

- 把一个文件拷贝到另外一个位置
- 把多个 JS 或者 CSS 文件合并成一个文件,以减少网络请求数
- 对JS文件和CSS进行合并压缩,以减少网络流量
- 把Sass或者Less文件编译成CSS
- 压缩图像文件,以减少网络流量
- 创建一个可以实时刷新页面内容的本地服务器等等。

> 只要你觉得有些动作是要重复去做的，一般你就可以把这些动作创建成一个gulp任务，然后在指定的条件下,比如文件发生变化以后,自动去执行这些任务。

### 1.2 gulp特点
- 易于使用 通过代码优于配置的策略，Gulp 让简单的任务简单，复杂的任务可管理。
- 快速构建 利用 node.js 流的威力，你可以快速构建项目并减少频繁的 IO 操作。前一级的输出，直接变成后一级的输入，使得在操作上非常简单
- 高质量的插件 Gulp 严格的插件指南确保插件如你期望的那样简洁地工作。
- 易于学习 通过最少的 API，掌握 Gulp 毫不费力，构建工作尽在掌握。

- 官方文档解释
* Stream 是 nodejs 各种对象实现的抽象接口。
* 比如标准输入是一个流，标准输出也是一个流。
* 所有的 stream 对象都是 EventEmitter 的实例,可以发射事件。
* 流是一种有起点和终点的数据传输手段。

- 上一个的输出，是下一个的输入
- 上一个的输出，是下一个的输入
- 上一个的输出，是下一个的输入

![图片地址](images/other01-gulp01.jpg)



### 1.3 gulp中的流

- gulp正是通过流和代码优于配置的策略来尽量简化任务编写的工作。
- 类似jquery里的链式操作，把各个方法串连起来构建完整的任务。
- 用gulp编写任务也可看作是用Node.js编写任务。
- 当使用流时，gulp不需要生成大量的中间文件，只将最后的输出写入磁盘，整个过程因此变得非常快。

### 1.4 安装node

- gulp是基于Nodejs的自动任务运行器
- 安装Gulp和相关行件用的都是node的包管理工具npm
- 所以你需要先在电脑上安装 node,确定在命令行工具的下面可以使用npm这个命令，这样就能去安装Gulp了。

> [node.js官网](https://link.juejin.im/?target=http%3A%2F%2Fwww.zhufengpeixun.cn%2Fcourse%2F19%2Flearn%23)

- 安装好以后，我们可以打开命令行工具，mac 用户可以使用终端工具，windows 用户可以找到cmd命令行工具。

### 1.5 安装gulp

在项目里使用gulp需要
* 在全局范围内去安装一下gulp的命令行工具
* 然后在项目里面再去本地安装gulp

### 1.6 gulp 命令行工具

- 使用 `npm install` 去安装 gulp，注意加上一个 `-g` 的参数，表示在全局范围内去安装.
- 一般用 npm 安装的时候用一个 `-g` 的参数就表示，这个安装的东西会作为命令去执行。
- 如果你在mac或linux下遇到了权限问题,在下面这个命令的前面加上 `sudo npm install gulp -g` 并输入mac密码。

> npm install -g gulp

安装完成后可以输入 `gulp --help`

如果输出一些帮助的信息就表示可以gulp命令行成功安装了

如果安装不上可以换一下源试试

- 淘宝源
	npm install -g gulp --registry=registry.npm.taobao.org
- 中国源
	npm install -g gulp --registry=registry.cnpmjs.org
- 官方源
	npm install -g gulp --registry=www.npmjs.org/


## 2. gulp 使用

### 2.1. 先创建一个目录

- 在 mac 和 linux 操作系统下执行

> mkdir learngulp

- 在 windows 操作系统下执行

> md learngulp

### 2.2 使用 命令进入此目录

> cd learngulp

### 2.3 创建项目描述文件 package.json

- **npm** ，需要一个叫 `package.json` 的文件来管理依赖，可以手工去创建这个文件，也可以使用 `npm init` 这个命令。 输入

> npm init

输入一些问题答案

```js
name: (zhufeng_automation) learngulp //项目名字，npm init会自动取当前目录名作为默认名字，这里不需要改，直接确认即可
version: (1.0.0) 1.0.0   //项目版本号，这个大家按自己习惯来定就可以
description: learn gulp //项目说明
entry point: (index.js) index.js // 入门文件 npm start 会执行此文件
test command: test.js //测试脚本 npm test 会执行此文件
git repository: (https://github/zhufengpeixun/zhufeng_automation.git) //模块的git仓库，选填。npm的用户一般都使用github做为自己的git仓库
keywords: node.js gulp  //在npmjs官网搜索时的关键字
author: zhangrenyang //项目作者名字
license: (ISC) MIT //授权协议
About to write to D:\mygit\zhufeng_automation\package.json:

{
  "name": "learngulp",
  "version": "1.0.0",
  "description": "learn gulp",
  "main": "index.js",
  "dependencies": {
    "gulp": "^3.9.0"
  },
  "devDependencies": {},
  "scripts": {
    "test": "test.js"
  },
  "repository": {
    "type": "git",
    "url": "https://git.coding.net/zhufengpeixun/zhufeng_automation.git"
  },
  "keywords": [
    "node.js",
    "gulp"
  ],
  "author": "zhangrenyang",
  "license": "MIT"
}


Is this ok? (yes) yes //对以上内容确认无误后，就可以直接回车确认了
```

回车后会在当前目录下创建一个 package.json 文件

这样可以把 gulp 作为项目的开发依赖(只在开发时用，不会发布到线上)，通过

> npm install gulp --save-dev

在node_modules下安装本地的gulp库并把添加配置到 `package.json` 文件里面。

```js
"devDependencies": {
    "gulp": "^3.9.0"
  }
```

### 2.4 创建配置文件：
gulp 的任务要放到一个叫 gulpfile.js 的文件里面，先在项目的根目录下面创建一个这样的文件。 然后在这个文件的顶部添加下面这行代码：

```js
var gulp = require('gulp');
```

通过require可以把gulp模块引入当前项目并赋值给gulp变量
这样，gulp 这个变量里面就会拥有 gulp 的所有的方法了

### 2.5 创建gulp的任务

可以使用gulp的task方法
同样我们去创建一个叫 hello 的任务，它要做的事就是在控制台上输出 "您好" 这两个字
第一个参数是任务的名称，第二个参数是任务的定义,是一个匿名函数

```js
gulp.task('hello', function () {
  console.log('您好');
});
```

执行 Gulp 的任务，打开命令行工具，进入到项目所在的目录，然后输入：


> gulp hello


会返回：

> $ gulp hello
> [21:36:34] Using gulpfile D:\mygit\zhufeng_automation\gulpfile.js
> [21:36:34] Starting 'hello'...
> 您好
> [21:36:34] Finished 'hello' after 959 μs


gulp后面跟着的是任务的名称，不输入任务名称的话会默认找default任务，找不到会报错

## 3 其它

### 3.1 其他任务

可以使用

> gulp \<task\> \<othertask\>

gulp 只有你需要熟知的参数标记，其他所有的参数标记只在一些任务需要的时候使用。

- -v 或 --version 会显示全局和项目本地所安装的 gulp 版本号
- --gulpfile 手动指定一个 gulpfile 的路径，这在你有很多个 gulpfile 的时候很有用。这也会将 CWD 设置到该 gulpfile 所在目录
- --cwd dirpath 手动指定 CWD。定义 gulpfile 查找的位置，此外，所有的相应的依赖（require）会从这里开始计算相对路径
- -T 或 --tasks 会显示所指定 gulpfile 的 task 依赖树
- --tasks-simple 会以纯文本的方式显示所载入的 gulpfile 中的 task 列表
- --color 强制 gulp 和 gulp 插件显示颜色，即便没有颜色支持
- --no-color 强制不显示颜色，即便检测到有颜色支持
- --silent 禁止所有的 gulp 日志


### 3.2 gulp.js工作方式

gulp的使用流程一般是：首先通过gulp.src()方法获取到想要处理的文件流，
然后把文件流通过pipe方法导入到gulp的插件中，
最后把经过插件处理后的流再通过pipe方法导入到gulp.dest()中，
gulp.dest()方法则把流中的内容写入到文件中。例如：

```js
var gulp = require('gulp');
 gulp.src('script/src.js')         // 获取文件的流的api
    .pipe(gulp.dest('dist/dest.js')); // 写文件的api
```

使用gulp，仅需知道4个API即可：gulp.task(),gulp.src(),gulp.dest(),gulp.watch()，所以很容易就能掌握

### 3.3 gulp.src()

在Gulp中，使用的是Nodejs中的stream(流)，首先获取到需要的stream，然后可以通过stream的pipe()方法把流导入到你想要的地方，比如Gulp的插件中，经过插件处理后的流又可以继续导入到其他插件中，当然也可以把流写入到文件中。所以Gulp是以stream为媒介的，它不需要频繁的生成临时文件，这也是Gulp的速度比Grunt快的一个原因。再回到正题上来，gulp.src()方法正是用来获取流的，但要注意这个流里的内容不是原始的文件流，而是一个虚拟文件对象流(Vinyl files)，这个虚拟文件对象中存储着原始文件的路径、文件名、内容等信息，这个我们暂时不用去深入理解，你只需简单的理解可以用这个方法来读取你需要操作的文件就行了。其语法为：

```js
gulp.src(globs[, options]) 
```

`globs`参数是文件匹配模式(类似正则表达式)，用来匹配文件路径(包括文件名)，当然这里也可以直接指定某个具体的文件路径。当有多个匹配模式时，该参数可以为一个数组。
`options`为可选参数。通常情况下我们不需要用到

### 3.4  glob语法
gulp内部使用了node-glob模块来实现其文件匹配功能。我们可以使用下面这些特殊的字符来匹配我们想要的文件：


### 3.5 gulp.dest()

gulp.dest()方法是用来写文件的，其语法为：

```js
 gulp.dest(path[,options]) 
```

path为写入文件的路径
options为一个可选的参数对象，通常我们不需要用到

要想使用好gulp.dest()这个方法，就要理解给它传入的路径参数与最终生成的文件的关系。

gulp的使用流程一般是这样子的：首先通过gulp.src()方法获取到我们想要处理的文件流，
然后把文件流通过pipe方法导入到gulp的插件中，最后把经过插件处理后的流再通过pipe方法导入到gulp.dest()中，
gulp.dest()方法则把流中的内容写入到文件中，
这里首先需要弄清楚的一点是，我们给gulp.dest()传入的路径参数，只能用来指定要生成的文件的目录，
而不能指定生成文件的文件名，它生成文件的文件名使用的是导入到它的文件流自身的文件名，
所以生成的文件名是由导入到它的文件流决定的，即使我们给它传入一个带有文件名的路径参数，
然后它也会把这个文件名当做是目录名，例如：

```js
 var gulp = require('gulp');
gulp.src('script/jquery.js')
.pipe(gulp.dest('dist/foo.js'));
//最终生成的文件路径为 dist/foo.js/jquery.js,而不是dist/foo.js 
```

要想改变文件名，可以使用插件 `gulp-rename`

下面说说生成的文件路径与我们给gulp.dest()方法传入的路径参数之间的关系。
gulp.dest(path)生成的文件路径是我们传入的path参数后面再加上gulp.src()中有通配符开始出现的那部分路径。例如：

```js
var gulp = reruire('gulp');

//有通配符开始出现的那部分路径为 `**/*.js`
gulp.src('script/**/*.js')
.pipe(gulp.dest('dist')); //最后生成的文件路径为 dist/**/*.js
//如果 **/*.js 匹配到的文件为 jquery/jquery.js ,则生成的文件路径为 dist/jquery/jquery.js 
```

再举更多一点的例子

```js
 gulp.src('script/avalon/avalon.js') //没有通配符出现的情况
.pipe(gulp.dest('dist')); //最后生成的文件路径为 dist/avalon.js

//有通配符开始出现的那部分路径为 **/underscore.js
gulp.src('script/**/underscore.js')
//假设匹配到的文件为script/util/underscore.js
.pipe(gulp.dest('dist')); //则最后生成的文件路径为 dist/util/underscore.js

gulp.src('script/*') //有通配符出现的那部分路径为 *
//假设匹配到的文件为script/zepto.js    
.pipe(gulp.dest('dist')); //则最后生成的文件路径为 dist/zepto.js 
```

通过指定gulp.src()方法配置参数中的base属性，我们可以更灵活的来改变gulp.dest()生成的文件路径。
当我们没有在gulp.src()方法中配置base属性时，base的默认值为通配符开始出现之前那部分路径，例如：

```js
gulp.src('app/src/**/*.css') //此时base的值为 app/src 
```

上面我们说的gulp.dest()所生成的文件路径的规则，其实也可以理解成，用我们给gulp.dest()传入的路径替换掉gulp.src()中的base路径，最终得到生成文件的路径。

```js
 gulp.src('app/src/**/*.css') //此时base的值为app/src,也就是说它的base路径为app/src
 //设该模式匹配到了文件 app/src/css/normal.css
.pipe(gulp.dest('dist')) //用dist替换掉base路径，最终得到 dist/css/normal.css 
```

所以改变base路径后，gulp.dest()生成的文件路径也会改变

```js
 gulp.src(script/lib/*.js) //没有配置base参数，此时默认的base路径为script/lib
 //假设匹配到的文件为script/lib/jquery.js
.pipe(gulp.dest('build')) //生成的文件路径为 build/jquery.js

gulp.src(script/lib/*.js, {base:'script'}) //配置了base参数，此时base路径为script
//假设匹配到的文件为script/lib/jquery.js
.pipe(gulp.dest('build')) //此时生成的文件路径为 build/lib/jquery.js     
用gulp.dest()把文件流写入文件后，文件流仍然可以继续使用。
```

### 3.6 gulp.task()
gulp.task方法用来定义任务，其语法为：

```js
gulp.task(name[, deps], fn) 
```

`name` 为任务名
`deps` 是当前定义的任务需要依赖的其他任务，为一个数组。当前定义的任务会在所有依赖的任务执行完毕后才开始执行。如果没有依赖，则可省略这个参数
`fn` 为任务函数，我们把任务要执行的代码都写在里面。该参数也是可选的。

```js
gulp.task('mytask', ['array', 'of', 'task', 'names'], function() { //定义一个有依赖的任务
    // Do something
}); 
```

gulp.task()这个API没什么好讲的，但需要知道执行多个任务时怎么来控制任务执行的顺序。
gulp中执行多个任务，可以通过任务依赖来实现。例如我想要执行one,two,three这三个任务，那我们就可以定义一个空的任务，然后把那三个任务当做这个空的任务的依赖就行了：

```js
//只要执行default任务，就相当于把one,two,three这三个任务执行了
gulp.task('default',['one','two','three']); 
```

如果任务相互之间没有依赖，任务会按你书写的顺序来执行，如果有依赖的话则会先执行依赖的任务。
但是如果某个任务所依赖的任务是异步的，就要注意了，gulp并不会等待那个所依赖的异步任务完成，而是会接着执行后续的任务。例如：

```js
gulp.task('one',function(){
  //one是一个异步执行的任务
  setTimeout(function(){
  console.log('one is done')
  },5000);
});
//two任务虽然依赖于one任务,但并不会等到one任务中的异步操作完成后再执行

gulp.task('two',['one'],function(){
  console.log('two is done');
}); 
```

上面的例子中我们执行two任务时，会先执行one任务，但不会去等待one任务中的异步操作完成后再执行two任务，而是紧接着执行two任务。所以two任务会在one任务中的异步操作完成之前就执行了。

那如果我们想等待异步任务中的异步操作完成后再执行后续的任务，该怎么做呢？
有三种方法可以实现：
第一：在异步操作完成后执行一个回调函数来通知gulp这个异步任务已经完成,这个回调函数就是任务函数的第一个参数。

```js
 gulp.task('one',function(cb){ //cb为任务函数提供的回调，用来通知任务已经完成
  //one是一个异步执行的任务
  setTimeout(function(){
    console.log('one is done');
    cb();  //执行回调，表示这个异步任务已经完成
  },5000);
});
//这时two任务会在one任务中的异步操作完成后再执行

gulp.task('two',['one'],function(){
  console.log('two is done');
}); 
```

第二：定义任务时返回一个流对象。适用于任务就是操作gulp.src获取到的流的情况。

```js
 gulp.task('one',function(cb){
  var stream = gulp.src('client/**/*.js')
      .pipe(dosomething()) //dosomething()中有某些异步操作
      .pipe(gulp.dest('build'));
    return stream;
});

gulp.task('two',['one'],function(){
  console.log('two is done');
}); 
```

第三：返回一个promise对象，例如

```js
 var Q = require('q'); //一个著名的异步处理的库 https://github.com/kriskowal/q
gulp.task('one',function(cb){
  var deferred = Q.defer();
  // 做一些异步操作
  setTimeout(function() {
     deferred.resolve();
  }, 5000);
  return deferred.promise;
});

gulp.task('two',['one'],function(){
  console.log('two is done');
}); 
```

gulp.task()就这些了，主要是要知道当依赖是异步任务时的处理。



### 3.7 gulp.watch()

gulp.watch()用来监视文件的变化，当文件发生变化后，我们可以利用它来执行相应的任务，例如文件压缩等。其语法为

```js
gulp.watch(glob[, opts], tasks) 
```

`glob` 为要监视的文件匹配模式，规则和用法与gulp.src()方法中的 `glob` 相同。
`opts` 为一个可选的配置对象，通常不需要用到
`tasks` 为文件变化后要执行的任务，为一个数组

```js
gulp.task('uglify',function(){
  //do something
});
gulp.task('reload',function(){
  //do something
});
gulp.watch('js/**/*.js', ['uglify','reload']); 
```

gulp.watch()还有另外一种使用方式：

```js
gulp.watch(glob[, opts, cb]) 
```

`glob`和 `opts` 参数与第一种用法相同
cb参数为一个函数。每当监视的文件发生变化时，就会调用这个函数,并且会给它传入一个对象，该对象包含了文件变化的一些信息，type属性为变化的类型，可以是 added , changed , deleted ； path 属性为发生变化的文件的路径

```js
 gulp.watch('js/**/*.js', function(event){
    console.log(event.type); //变化类型 added为新增,deleted为删除，changed为改变 
    console.log(event.path); //变化的文件的路径
}); 
```




1. 导入gulp
打开 gulpfile.js ，在这里先去创建一个对象，叫 gulp ，让它等于 require('gulp');
这样这个 gulp 对象就拥有了 gulp 提供的所有属性还有方法了。

2. 创建源文件
mkdir app
在app下创建 index.html
3. 任务目标
然后用 gulp 的 task 方法，去创建一个任务，
这个任务要做的事就是把我们项目里的app下的index.html 这个文件，复制到一个叫 dist 的目录里面，这个 dist 目录表示的是 distribution,也就是正式发新版。

4. 编写任务
先给这个任务起个名字 ... 可以叫它 copy-html
再写一个匿名函数
先用写 return
大部分的 gulp 任务，首先要做的就是去读取要处理的文件,读取文件用的是 src 这个方法,在这个方法里，指定一下要读取的文件 index.html
找到要处理的文件以后，再用一个 pipe方法，你可以把这个 pipe 想像成是一个管道， 把文件读取进来，放到一个管道里，在这个管道里面，你可以使用 gulp 的插件去处理读取进来的文件
因为这里我们只是简单的把文件保存到一个指定的地方，所以不需要使用插件，可以使用 gulp 的 dest 这个方法，在这个方法里，指定一下文件要存储到的那个位置。
这样我们就创建好了这个把单个文件复制到指定位置的任务
5. 执行
打开命令行工具
先确定当前的位置是在项目的目录里面
然后输入 gulp+后面加上任务的名字

gulp copy-html
输入回车，会出现一些提示：

使用的 gulpfile 的位置
开始执行的任务
还有任务结束所花的时间
代码
 var gulp = require('gulp');
 gulp.task('copy-html',function(){
     return gulp.src('app/index.html').pipe(gulp.dest('dist'));
 });




1. 导入gulp
打开 gulpfile.js ，在这里先去创建一个对象，叫 gulp ，让它等于 require('gulp');
这样这个 gulp 对象就拥有了 gulp 提供的所有属性和方法了。

2. 创建源文件
在app下创建


3. 任务目标
然后用gulp的task方法,去创建一个任务，
把imgs目录里的文件复制到dist这个目录的下面

4. 编写任务
先给这个任务起个名字 ... 可以叫它 copy-imgs
再写一个匿名函数
先写 return
大部分的 gulp 任务，首先要做的就是去读取要处理的文件,读取文件用的是 src 这个方法
'app/imgs/*.png' 指app/imgs/这个目录里面的所有的.png格式的图片,这个 * 号表示的就是任何东西. *.png 意思就是，不管图片的文件名是什么，只要它是 .png 格式的就行.
gulp.src('app/imgs/*.png')
5. 执行
打开命令行工具
先确定当前的位置是在项目的目录里面
然后输入 gulp+后面加上任务的名字

gulp copy-imgs
输入回车，会出现一些提示：

使用的 gulpfile 的位置
开始执行的任务
还有任务结束所花的时间
完成以后，你会看到，在项目的dist这个目录里面，会创建一个叫imgs的目录,在这个目录里面，有两张图片1.png 2.png它们都是从项目根目录下的imgs这个目录里面复制过来的.
在这个目录里面，这张jpg格式的图片，还有small里面的图片，并没有复制到dist下面的 imgs 目录里面。因为我们写的glob只匹配imgs目录下的所有的.png格式的图片

6.指定多个后缀
如果你想把 imgs 目录下面的所有的图像文件都复制到 dist 下面的 imgs 目录里面，在这个 src 方法的 glob 里面，可以指定多个扩展名,现在是 *.png, 后面加上一组花括号,在这个花括号里面，指定多个扩展名.{jpg,png}注意逗号的后面不要使用空格.

多个glob
有些任务你可能需要用到多个glob，这样我们就可以用一个数组，数组里的每个项目表示的就是用来匹配文件的glob。
比如我们的项目里有两个目录，css还有js。
每个目录下面都有一些文件。
我们想创建一个任务，需要用到这两个目录里面的东西。
在这个任务里，我们就可以使用多个glob。

    ['app/css/*.css','app/js/*.js']
数组里有两个glob
再次执行任务
会发现glob中的文件都拷贝到dist下面去了

排除特定文件
在 glob 的前面，再加上一个!号，表示这是要排除掉的文件

['app/css/*.css','app/js/*.js','!app/js/*.tmp.js']
代码
var gulp = require('gulp');

/**
 * 复制图片
 */
gulp.task('copy-images',function(){
    return gulp.src('app/imgs/*.jpg').pipe(gulp.dest('dist'));
});

/**
 * 1. {} 里可以指定多个扩展名
 * 2. * 匹配所有的字符，除了路径分隔符 /
 * 3. ** 匹配所有的字符，包括路径分隔符 /
 */
gulp.task('copy-images',function(){
      return gulp.src('app/imgs/**/*.{jpg,png}').pipe(gulp.dest('dist'));
});

/**
 * 匹配多个目录 glob
 * 可以填写一个数组
 *
 */
gulp.task('copy-other',function(){
    return gulp.src(['app/css/*.css','app/js/*.js'],{base:'app'}).pipe(gulp.dest('dist'));
});

/**
 * 匹配多个目录 glob
 * ! 排除一个文件
 *
 */
gulp.task('copy-other',function(){
    return gulp.src(['app/css/*.css','app/js/*.js','!app/js/*.tmp.js'],{base:'app'}).pipe(gulp.dest('dist'));
});


1. 组合任务
在创建 gulp 任务的时候，我们可以去给任务指定它依赖的其它的任务。
比如，这里我们创建了三个任务，copy-html，copy-imgs，copy-other。
我们想再创建一个叫 build 的任务，这个任务依赖这里的这三个任务。

2. 编写
使用gulp的task这个方法去创建任务
先给这个任务起个名字,叫做 build.
再把这个方法的第二个参数设置成一个数组,这个数组里的项目就是这个任务所依赖的任务,输入一组方括号,再把它需要的三个任务，作为这个数组的三个项目.
我们可以继续去设计这个任务要作的事情，用一个匿名函数,
可以让它在控制台上输出 编译成功 ,这样在执行 build 任务的时候，会先去执行它依赖的三个任务，最后再执行它本身要做的任务。

3. 执行
保存,打开命令行工具,输入 gulp build,回车.
注意这里会同时去执行 build 需要的三个任务，并不是先执行一个，等待完成以后再去执行一个，
这些依赖的任务是同时执行的,等它们都完成以后，才会执行 build 本身要做的任务，这里就是在控制台上，输出编译成功 这几个字儿。

代码
var gulp = require('gulp');

gulp.task('copy-html',function(){
    return gulp.src('app/index.html').pipe(gulp.dest('dist'));
});

gulp.task('copy-images',function(){
    return gulp.src('app/imgs/**/*.{jpg,png}').pipe(gulp.dest('dist'));
});

/**
 * 匹配多个目录 glob
 * ! 排除一个文件
 *
 */
gulp.task('copy-other',function(){
    return gulp.src(['app/css/*.css','app/js/*.js','app/js/*.tmp.js'],{base:'app'}).pipe(gulp.dest('dist'));
});


gulp.task('default',['copy-html','copy-images','copy-other'],function(){
    console.log('全部拷贝任务执行完毕!');
});
1. 监听任务
使用 gulp 的 watch 这个方法，我们可以去监视一些文件，当这些文件发生变化的时候，立即去执行一些指定的任务

2.编写
先打开 gulpfile.js,再去创建一个任务
gulp.task,这个任务可以叫做 watch,再用一个匿名函数,在它里面，再用 gulp 的 watch 方法去做点事情。

输入 gulp.watch(),先指定一下要监视的文件,比如去监视 index.html
再把要执行的任务列表放到这里，这个任务列表要放到一个数组里，所以先输入一组方括号，要执行的任务是 copy-html.
它的意思就是，我们在执行 watch 任务的时候，去监视 index.html 这个文件的变化，当这个文件发生变化以后，就去自动执行 copy-html 这个任务。

执行
保存 回到命令行工具
先去执行一下刚才创建的 watch 这个任务 gulp watch ,这样 gulp 就会去监视文件的变化了,你会看到这个任务并没有立即结束,它会一直运行,直到我们手工退出这个任务,退出可以按一上 ctrl + C
再回到项目,打开 index.html 这个文件,随便修改一个地方,然后保存一下,回到命令行,你会看到 gulp 执行了 copy-html 这个任务，因为 index.html 这个文件发生了变化

每次保存被监视的文件，都会去执行指定的任务列表。
回到项目，打开 dist 下面的 index.html,你会看到修改之后的 index.html 已经被复制到了这个目录的下面.

代码
var gulp = require('gulp');

gulp.task('copy-html',function(){
    return gulp.src('app/index.html').pipe(gulp.dest('dist'));
});

gulp.task('copy-images',function(){
    return gulp.src('app/imgs/**/*.{jpg,png}',{base:'app'}).pipe(gulp.dest('dist'));
});

/**
 * 匹配多个目录 glob
 * ! 排除一个文件
 *
 */
gulp.task('copy-other',function(){
    return gulp.src(['app/css/*.css','app/js/*.js','app/js/*.tmp.js'],{base:'app'}).pipe(gulp.dest('dist'));
});


//在执行watch的时候会监控index.html文件的变化，发生变化后可以执行拷贝html的任务
gulp.task('default',function(){
    gulp.watch('app/index.html',['copy-html']);
    gulp.watch('app/imgs/**/*.{jpg,png}',['copy-images']);
    gulp.watch(['app/css/*.css','app/js/*.js','app/js/*.tmp.js'],['copy-other']);
});


gulp插件
gulp提供了一些很实用的接口，但本身并不能做太多的事情。
可以读取文件、写入文件以及监控文件等一少部分功能。
其它实用的功能都是依靠插件来进行扩展的。
这些插件可以实现比如

编译 Sass：gulp-sass
编译 Less：gulp-less
合并文件：gulp-concat
压缩js 文件：gulp-uglify
重命名js文件：gulp-rename
优化图像大小：gulp-imagemin
压缩css 文件：gulp-minify-css
创建本地服务器：gulp-connect
实时预览 gulp-connect
插件列表
gulp插件

使用插件
npm install xxx --save-dev 安装插件
在 gulpfile.js 顶部引入此插件
在创建任务的时候使用此插件




自动加载gulp 插件
gulp-load-plugins这个插件能自动帮你加载package.json文件里的gulp插件。
例如假设你的package.json文件里的依赖是这样的:

"devDependencies": {
   "gulp": "^3.9.0",
   "gulp-concat": "^2.6.0",
   "gulp-connect": "^2.2.0",
   "gulp-imagemin": "^2.3.0",
 }
然后我们可以在gulpfile.js中使用gulp-load-plugins来帮我们加载插件：

var gulp = require('gulp');
//加载gulp-load-plugins插件，并马上运行它
var $ = require('gulp-load-plugins')();
然后我们要使用gulp-rename和gulp-ruby-sass这两个插件的时候，
就可以使用$.concat和$.connect来代替了,也就是原始插件名去掉gulp-前缀，之后再转换为驼峰命名。



less
less插件可以把less文件编译成css

less任务
可以在app/less下面创建文件page.less,然后就可以把此文件编译到dist下面

安装插件
    npm install gulp-less --save-dev
安装后可以在node-modules里看到此插件
也可以在package.json的devDependencies里面看到此插件的配置

代码如下
var gulp = require('gulp');
var less = require('gulp-less');

gulp.task('less',function(){
    return gulp.src('app/less/*.less').pipe(less()).pipe(gulp.dest('dist/css'));
});

gulp.task('default',['less']);




sass
想要使用 Gulp 去把 Sass 编译成 CSS ，我们可以使用 gulp-sass 这个插件。

插件任务
可以在app/sass下面创建文件base.scss,然后就可以把此文件编译到dist下面

安装插件
npm install gulp-sass --save-dev
安装后可以在node-modules里看到此插件

也可以在package.json的devDependencies里面看到此插件的配置 "gulp-sass": "^2.0.4"

使用插件
在项目里面，app/sass 这个目录的下面，有一个sass文件，就是这个base.scss

$blue : #1875e7;　
　　div {
　　　color : $blue;
　　}
下面，我们可以使用gulp-sass这个插件，把这个目录里面的sass文件编译成css ，
再放到 dist 目录下面的 css 这个目录的下面。

代码如下
var gulp = require('gulp');
var sass = require('gulp-sass');

gulp.task('sass',function(){
    return gulp.src('app/sass/*.scss').pipe(sass()).pipe(gulp.dest('dist/css'));
});

gulp.task('default',['sass']);


gulp-connect
有些时候我们需要把文件放到本地服务器上去预览，gulp-connect可以帮我们创建一个本地服务器去运行我们的项目

安装插件
     npm install gulp-connect --save-dev
加上一个 --save-dev，把这个插件放到开发依赖里面。

创建任务
打开 gulpfile.js
先在文件的顶部这里
去包含一下这个 gulp-connect 插件
给它起个名字connect ...
var connect = require('gulp-connect');

代码如下
    var gulp = require('gulp');
    var connect = require('gulp-connect');
    
    gulp.task('server',function(){
       connect.server({
           root:'dist',//服务器的根目录
           port:8080 //服务器的地址，没有此配置项默认也是 8080
       });
    });
      
    gulp.task('default',['server']); //运行此任务的时候会在8080上启动服务器，
gulp-connect
我们希望当文件变化的时候浏览器可以自动刷新，这样我们就不需要文件修改后手动去刷新浏览器了

代码如下
var gulp = require('gulp');
var connect = require('gulp-connect');

gulp.task('copy-html',function(){
     gulp.src('app/index.html')//指定源文件
         .pipe(gulp.dest('dist'))//拷贝到dist目录
         .pipe(connect.reload());//通知浏览器重启
});

gulp.task('watch',function(){
    gulp.watch('app/index.html',['copy-html']);//当index.html文件变化时执行copy-html任务
});

gulp.task('server',function(){
    connect.server({
        root:'dist',//服务器的根目录
        port:8080, //服务器的地址，没有此配置项默认也是 8080
        livereload:true//启用实时刷新的功能
    });
});
gulp.task('default',['server','watch']);//运行此任务的时候会在8080上启动服务器，


gulp-concat
这个插件可以把几个文件合并到一块

安装
npm install gulp-concat --save-dev  
代码如下
var gulp = require('gulp');
var concat = require('gulp-concat');

gulp.task('concat',function(){
    return gulp.src(['app/js/*.js','!app/js/*.tmp.js'])//指定要合并的文件glob
        .pipe(concat('app.js'))//进行合并并指定合并后的文件名
        .pipe(gulp.dest('dist/js'));//输出到目标路径
});

gulp.task('default',['concat']);


gulp-concat
合并后我们可以对JS文件进行合并，最小化处理

安装
先打开命令行安装

    npm install gulp-uglify --save-dev
代码如下
var gulp = require('gulp');
var concat = require('gulp-concat');
var uglify = require('gulp-uglify')

gulp.task('uglify',function(){
    return gulp.src(['app/js/*.js','!app/js/*.tmp.js'])
        .pipe(concat('app.js')) //把多个JS文件合并成一个文件
        .pipe(uglify()) //对合并后的app.js文件进行压缩
        .pipe(gulp.dest('dist/js')); //输出到目的地
});

gulp.task('default',['uglify']);




html文件压缩
gulp-minify-html插件用来压缩html文件。

代码如下
var gulp = require('gulp'),
    minifyHtml = require("gulp-minify-html");

gulp.task('minify-html', function () {
    gulp.src('src/*.html') // 要压缩的html文件
    .pipe(minifyHtml())    //压缩
    .pipe(gulp.dest('dist/html'));//输出到目的地
});




gulp-rename
在把处理好的文件存放到指定的位置之前，我们可以先去重新命名一下它。可以使用gulp-rename这个插件.

安装
    npm install gulp-rename --save-dev
代码如下
var gulp = require('gulp');
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');
var rename = require('gulp-rename');
gulp.task('uglify',function(){
    return gulp.src(['app/js/*.js','!app/js/*.tmp.js'])//指定要处理的文件
        .pipe(concat('app.js'))//合并成一个文件
        .pipe(gulp.dest('dist/js'))//保存此文件
        .pipe(uglify())//进行压缩
        .pipe(rename('app.min.js'))//对此文件进行重命名
        .pipe(gulp.dest('dist/js'));//再输出一次
});

gulp.task('default',['uglify']);




gulp-minify-css
如果要想压缩css,我们可以使用gulp-minify-css

安装
    npm install gulp-minify-css --save-dev
代码如下
var gulp = require('gulp');
var less = require('gulp-less');
var minify = require('gulp-minify-css');//在文件的顶部去包含这个插件，起个名字，叫做 minify
var rename = require('gulp-rename');
gulp.task('minify',function(){
    return gulp.src('app/less/page.less')//指定 less文件
        .pipe(less())//把less编译成css
        .pipe(gulp.dest('dist/css'))//输出到目的地
        .pipe(minify())//对 css再进行压缩
        .pipe(rename('page.min.css'))//重命名
        .pipe(gulp.dest('dist/css'));//输出到目的地
});

gulp.task('default',['less']);




gulp-imagemin
如果要想在保证不改变图像质量的情况下，让图像文件的体积变得更小一点,我们可以使用gulp-imagemin

安装
    npm install gulp-imagemin --save-dev  
代码如下
var gulp = require('gulp');
var imagemin = require('gulp-imagemin');

gulp.task('copy-images',function(){
    return gulp.src('app/imgs/**/*.{jpg,png}')//指定要压缩的图片
        .pipe(imagemin()) //进行图片压缩
        .pipe(gulp.dest('dist'));//输出目的地
});

gulp.task('default',['copy-images']);




jshint
可以用此插件进行代码检查

安装
npm install gulp-jshint --save-dev
代码
    var gulp = require('gulp'),
        jshint = require("gulp-jshint");
     
    gulp.task('jsLint', function () {
        gulp.src('src/*.js')
        .pipe(jshint()) //进行代码检查
        .pipe(jshint.reporter()); // 输出检查结果
    });





DEMO :
{
  "name": "tongbanke",
  "version": "1.0.0",
  "description": "tobanke'",
  "main": "main.js",
  "scripts": {
    "test": "test"
  },
  "repository": {
    "type": "git",
    "url": "gulp"
  },
  "keywords": [
    "gulp",
    "test"
  ],
  "author": "kongzhi",
  "license": "ISC",
  "devDependencies": {
    "gulp": "^3.6.2",
    "gulp-coffee": "^1.4.2",
    "gulp-concat": "^2.6.0",
    "gulp-connect": "^2.3.1",
    "gulp-jshint": "^2.0.4",
    "gulp-less": "^3.1.0",
    "gulp-obfuscate": "^0.2.9",
    "gulp-uglify": "^2.0.0",
    "gulp-watch": "^0.6.2",
    "jshint": "^2.9.3"
  }
}





var gulp = require('gulp');
var concat = require('gulp-concat'); //文件合并
var uglify = require('gulp-uglify'); //文件压缩
var rename = require('gulp-rename'); //文件重命名
var obfuscate = require('gulp-obfuscate'); //代码混淆
var connect = require('gulp-connect');  //创建一个本地服务器
jshint = require("gulp-jshint");   //语法校验
// 语法检查

gulp.task('jshint', function() {
	console.log('语法检查...');
	return gulp.src('src/*.js')
		.pipe(jshint())    //进行代码检查
		.pipe(jshint.reporter('default')); // 输出检查结果
});
//创建一个本地服务器
gulp.task('server',function(){
	console.log("创建本地服务器！")
       connect.server({
       	   livereload:true,//启用实时刷新的功能
           root:'./',//服务器的根目录
           port:12306 //服务器的地址，没有此配置项默认也是 8080
       });
    });
// 合并文件之后压缩代码
gulp.task('minify', function() {
	console.log('压缩合并');
	return gulp.src('src/*.js')  //指定要合并的文件glob
		.pipe(concat('main.js'))  //进行合并并指定合并后的文件名
		.pipe(gulp.dest('min.js'))  //输出到目标路径
		.pipe(uglify())
		.pipe(rename('main.min.js'))
		.pipe(connect.reload())  //通知浏览器重启
		.pipe(gulp.dest('min.js'));

});

// 监视文件的变化
gulp.task('watch', function() {
	console.log('文件有变动');
	gulp.watch('src/*.js', ['minify','jshint'],function(event){
		 console.log(event.type); //变化类型 added为新增,deleted为删除，changed为改变 
         console.log(event.path); //变化的文件的路径
	});
});

// 注册默认任务
gulp.task('default', ['minify', 'watch','server', 'jshint'], function() {
	console.log('压缩合并混淆重命名');
	return gulp.src('main.min.js')
		.pipe(obfuscate()); //压缩完代码混淆
});







温馨提示：语法检查慎用！！！