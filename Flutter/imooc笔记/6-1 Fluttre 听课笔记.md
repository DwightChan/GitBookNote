


快捷键 com + n + enter 调出需要重写的方法


# StatelessWidget 和 StatefulWidget 的区别

```txt


```

# 6-4 视频

## StatelessWidget 相关组件 和 装饰器
1. Scaffold 是什么组件
2. BoxDecoration 装饰器
3. Chips 是材料设计的一个小部件，可以查 材料设计的相关图片
4. Divider 分割线
5. Card 卡片， 在列表功能中较常见
6. AlertDialog 弹框；

# 6-5 视频

## StatefulWidget 常用的基础组件
1. MaterialApp, 继承 自 StatefulWidget
   1. app
2. Scaffold
   1. 完整的页面 
   2. appBar
   3. bottomNavigationBar
   4. body

3. AppBar
4. BottomNavigationBar
5. RefreshIdicator
6. Image
7. TextField
8. PageView
9.  

设置 bottom navigationBar 的选中状态
通过 setState(() {
    _currentIndex = Index
})
切换页面
body: _currentIndex == 0 ? Contain.. : Text("文本")

悬浮按钮
floatingActionButton: FloatingActionButton 

刷新组件 RefreshIdicator 一定是要和列表配合使用

RefreshIdicator(child: ListView(children<Widget>: Countainer()), onRefresh: __handleRefresh)

Future<Null> _handleRefresh() async(
    await Future.delayed(Duration(milliseconds: 200));
    return null;
)


Image 
TextField 继承自 StatefulWidget

PageView 就是轮播图组件
通常放在 Container 中，并使用 Container 来约束起大小


# 6-6 Flutter布局组件

1. Container
2. RederObjectWidget


   1. SingleChildRederObjectWidget 单节点
      1. Opacity 透明度
      2. ClipOval 裁剪为圆形
      3. ClipRRect 裁剪为方型
      4. PhysicalModel 显示为不同形状的组件
      5. Alige center 剧中
      6. Padding 边距
      7. SizeBox 大小
      8. FractionallySizeBox 水平/ 垂直 等伸缩 撑满
   
   2. MultiChildRenderObjectWidget 多节点
      1. Stack 层叠布局
      2. Flex 
         1. Column 垂直排列
         2. Row 水平排列 （不能换行）
      3. Wrap 包裹 可以换行
      4. Flow 浮动
3. ParentDataWidget
   1. Positioned 位置
   2. Flexible
      1. Expanded 展开

# 6-7 flutter 的路由与导航

routes 是MeaterialApp 的属性
有两种 push 方式 
1. 根据路由名称
2. 根据别名

RaisedButton 按钮

# 6-8 如何检查用户手势 以及处理点击事件

GestureDetector 手势组件
onTap
onDoubleTap
onLongPress
onTapCancel
onTapUp
onTapDown

Positioned 设置 位置 需求 跟着手指滑动的小球
left: _moveX
top: _moveY

onPanUpdate 更新拖拽位置


setState 设置状态 在RN  在hook 之前都是用 setState 


# 6-9 导入和使用 flutter 的资源文件；
1. 需要在pubspec.yaml 文件中 assets 配置；
2. 使用 Image( image: Asset)

# 6-10 flutter 打开第三方app
插件 url_launcher



# 6-11 Flutter 页面生命周期实战指南

生命周期必备考点

1. StatelessWidget
2. StatefulWidget
   1. 初始化时期
      1. ceacteState 
      2. initState （经常用到）
   2.  更新
       1. didChangedependencies 必须调用父类的方法，在依赖的的 State 改变的时候调用， InheritedWidget 数据共享树；
       2.  build 数据更新都会调用（经常用到）
       3.  didUpdateWidget
   3. 销毁
      1. deactivate 很少被 使用 ， 在dispose之前被调用
      2. dispose 组件被销毁的 时候调用 （经常用到）

- **InheritedWidget** 概念需要理解并记住


# 6-12 flutter 应用的生命周期
1. 需要用到 widegetsBindingObserver 是一个Widgets 绑定观察期。通过它可以观察到应用到生命周期
WidgetsBinding.instance.addObserver(this);

2. didChangeAppLifecycleState 
3. 在dispose 的时候需要 移除监听
   1. WidgetsBinding.instance.removeObserver(this);

# 6-13 如何修改Flutter 应用的主题
通过 ThemeData 组件修改

# 6-14 如何自定义字体？
在 pubspec.yaml 中添加配置

fonts:
  - family: 定义字体的名字
    fonts:
      - asset: 存放路径 相对路径；

在需要用到的地方使用 该字体
在 Theme ThemeData 中 fontFamily 设置室应用到全局；
在指定位置使用TextStyle 组件 修饰 fontFamily 属性赋值字体名称


# 6-15/16 拍照app拍照配置与Androidx 兼容处理
- image_picker 拍照插件 谷歌提供的 （需要安卓项目现兼容 Androidx ）
  - Androidx 兼容 解决方法 在 flutter 文档有体现；
  - iOS 需要 在info.plist 文件中配置权限；