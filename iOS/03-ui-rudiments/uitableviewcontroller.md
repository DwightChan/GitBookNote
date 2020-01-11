# UITableViewController

- tableVieController 有个 tableView 属性, strong 指向 tableView,
- 而tableView的dataSource和delegate属性指向就是这个控制器.
- 并且这个控制器已经遵守了UITableViewDataSource和UITableViewDelegate协议.
- 每个控制器的内部都有一个view属性,
- 在tableVieController中,view和tableView属性指向的是同一个对象.