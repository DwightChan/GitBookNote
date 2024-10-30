


# 8-2 app 首页框架搭建

# 8-3 tabbar 结构 框架 代码代码实践

- Scaffold 用于布局 tabbar 下的框架 
- PageView 用于包裹多个 分页，例如 首页、搜索、我的、旅游 等等多个控制器页面；
- PageController 控制显示 第几个控制器
- 

# 8-4 轮播图 banner 功能开发

- flutter-swiper 第三方插件
  
# 8-5 自定AppBar 实现滚动渐变

- ListView 自动有安全距离
  - 使用 MediaQuery.removePadding 组件的对应反复 可以移除 安全距离；可以指定 移除对应边的安全距离；
- NotificationListener 包裹ListView 可以监听 滚动；
  - NotificationListener 可以监听内部所有组件 包括子元素内的
  - 方法 onNotification 方法 和 对应的形参 的属性配合
    - 例如 形参 params； param.depth 深度
  - 注意没有滚动的时候也会定时回调 因此需要手动过滤 update 类型才处理

- Opacity 可以透明的组件
  - 