

# 10-2 基于 ListView 实现水平和垂直方式滚动的列表

### ListView 和 ListViewBuilder 

1. ListView 是一个通用的滚动列表组件，适用于列表项数量较少的情况。它可以直接接受一个子组件列表。
2. ListView.builder 是一个更高效的列表组件，适用于列表项数量较多或无限的情况。它通过一个回调函数按需生成列表项。

3. list UI 显示
4. list 点击事件
5. 默认是 垂直方向
6. scrollDirection 设置 滚动方向


# 10-3 基于ExpansionTile实现可展开的列表

- 使用 ExpansionTile 来显示 ListView 的每个 item 既可以

# 10-4 基于GridView实现网格布局

- GridView.count 创建 网格组件；

# 10-5 高级功能列表下拉刷新与上拉加载更多功能实现

- 使用 RefreshIndicator 包裹ListView 即可 实现下拉刷新；
- 使用 ScrollController 可以实现上拉加载更多；

```
ScrollController _scrollController = ScrollController();

  @override
  void initState() {
    _scrollController.addListener(() {
      if (_scrollController.position.pixels ==
          _scrollController.position.maxScrollExtent) {
        _loadData();
      }
    });

    super.initState();
  }
```
- 注意 定义的 控制器 一定要关联到对应的listView 才生效
```
ListView(
            controller: _scrollController,
            children: _buildList(),
          )
```

- 注意 添加了 监听 就需要 移除 
```
  @override
  void dispose() {
    _scrollController.dispose();
    super.dispose();
  }
```
