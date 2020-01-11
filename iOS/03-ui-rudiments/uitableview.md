# UITableView的基本使用

##本节知识点
1. [UITabView的介绍](#UITabView的介绍)
2. [UITableView的常见属性](#UITableView的常见属性)
3. [UITableView设置数据源/实现数据源方法](#UITableView设置数据源/实现数据源方法)
4. [UITableView设置代理以及代理方法](#UITableView设置代理以及代理方法)
5. [UITableView的性能优化](#UITableView的性能优化)
* [UITableView的索引条](#UITableView的索引条)

---

## <a id="UITabView的介绍"></a>1. UITabView的介绍

- 在iOS中，要实现展示列表数据，最常用的做法就是使用UITableView
- UITableView继承自UIScrollView，因此支持垂直滚动，而且性能极佳


- **UITableView的两种样式**
  - UITableViewStylePlain
  - UITableViewStyleGrouped


---

## <a id="UITableView的常见属性"></a>2. UITableView的常见属性

- **设置每一行cell的高度,(默认是 44)**
```objc
self.tableView.rowHeight
```

- **设置每一组头部的高度**
```objc
self.tableView.sectionHeaderHeight
```

- **设置每一组尾部的高度**
```objc
self.tableView.sectionFooterHeight 
```

- **设置分割线颜色**
```objc
self.tableView.separatorColor = [UIColor redColor];
```

- **设置分割线样式**
```objc
self.tableView.separatorStyle = UITableViewCellSeparatorStyleNone;
```

- **设置表头控件**
```objc
self.tableView.tableHeaderView = [[UISwitch alloc] init];
```

- **设置表尾控件**
```objc
self.tableView.tableFooterView = [UIButton buttonWithType:UIButtonTypeContactAdd];
```

- **设置右边索引文字的颜色**
```objc
self.tableView.sectionIndexColor = [UIColor redColor];
```

- **设置右边索引文字的背景色**
```objc
self.tableView.sectionIndexBackgroundColor = [UIColor blackColor];
```

- **设置估算高度**
```objc
// 给 每一行 cell 设置估计高度
self.tableView.estimatedRowHeight = 150;
```

- **注意: 如果设置 tableView 的估算高度, 会影响`tableView:heightForRowAtIndexPath:`代理方法的调用次数**
    - 如果设置了估算高度estimatedRowHeight
        - `tableView:heightForRowAtIndexPath:`代理方法的调用只会在每个 cell 要显示的时候跟随数据源方法`tableView: cellForRowAtIndexPath:`的后面成对被调用
    - 如果没有设置估算高度estimatedRowHeight
        - `tableView:heightForRowAtIndexPath:`代理方法是每当加载tableView 的数据时(包括reloadData)都会调用，有多少条数据，就会调用多少次这个方法(比如一共有100条数据，就会调用100次这个方法),用于先计算 tableView 的内容 contentSize 大小(可滚动范围), 只有这里先计算出 contentSize 之后才会出现下面调用给 cell 设置数据的数据源方法;
        - 每当有 cell 需要显示在视野范围时，`tableView:heightForRowAtIndexPath:`代理方法都会跟随数据源方法`tableView: cellForRowAtIndexPath:`后面成对被调用
    - 设置估算高度 **优点**
        - 减少heightForRowAtIndexPath方法的调用次数
        - 可以让暂时看不见的cell的高度延迟计算
    - 设置估算高度 **缺点**
        - contentSize的不太准确的
        - 滑动过程中，滚动条的长度会变来变去（可能会有跳跃效果）
        - 因此, 如果 contentSize 的要求严格, 使用 contentSize 的实际值有特别的用意, 则最后不要设置估算高度 ;


---

## <a id="UITableView设置数据源/实现数据源方法"></a>3. UITableView设置数据源/实现数据源方法

- **设置数据源对象**
    - 一般情况控制器就是它的数据源

  ```objc
  self.tableView.dataSource = self;      
  ```	
    
- **数据源对象要遵守协议**

  ```objc
  @interface ViewController () <UITableViewDataSource>
  @end
  ```


- **实现数据源方法**


- 设置分组数，返回值就是要设置的分组数（该方法不实现就默认是一组）

  ```objc
  - (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView;
  ```

- 设置每组的行数，返回值就是行数

  ```objc
  - (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section;
  ```

- 设置每组显示的内容，返回值就是要设置的内容（对象）

  ```objc
  - (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath;
  // 返回类型是 UITableViewCell 类 或者 子类
  ```

- 设置每组头部显示的内容，返回值就是要设置的内容（对象）

  ```objc
  - (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section;
  ```

- 设置每组尾部显示的内容，返回值就是要设置的内容（对象）

  ```objc
  - (NSString *)tableView:(UITableView *)tableView titleForFooterInSection:(NSInteger)section
  ```


---

## <a id="UITableView设置代理以及代理方法"></a>4. UITableView设置代理以及代理方法
- **实现代理源方法**
    - 一般情况控制器就是它的代理
    - 代理一般用于监听tableView 中 cell 或者其他属性的变化情况

  ```objc
  self.tableView.delegate = self;      
  ```	
    
- **数据源对象要遵守协议**

  ```objc
  @interface ViewController () <UITableViewDataSource,UITableViewDelegate>
  @end
  ```

- **(代理)实现代理方法**
    - 代理协议遵循超类(基类)以及父类的代理协议(`<NSObject, UIScrollViewDelegate>`)
    - 这里所有的代理方法都是可选择性实现

  ```objc
  @protocol UITableViewDelegate<NSObject, UIScrollViewDelegate>

  @optional
  ```

- 即将显示/结束显示时调用下面这些方法

  ```objc
  // Display customization
  - (void)tableView:(UITableView *)tableView willDisplayCell:(UITableViewCell *)cell forRowAtIndexPath:(NSIndexPath *)indexPath;
  - (void)tableView:(UITableView *)tableView willDisplayHeaderView:(UIView *)view forSection:(NSInteger)section NS_AVAILABLE_IOS(6_0);
  - (void)tableView:(UITableView *)tableView willDisplayFooterView:(UIView *)view forSection:(NSInteger)section NS_AVAILABLE_IOS(6_0);
  - (void)tableView:(UITableView *)tableView didEndDisplayingCell:(UITableViewCell *)cell forRowAtIndexPath:(NSIndexPath*)indexPath NS_AVAILABLE_IOS(6_0);
  - (void)tableView:(UITableView *)tableView didEndDisplayingHeaderView:(UIView *)view forSection:(NSInteger)section NS_AVAILABLE_IOS(6_0);
  - (void)tableView:(UITableView *)tableView didEndDisplayingFooterView:(UIView *)view forSection:(NSInteger)section NS_AVAILABLE_IOS(6_0);
  ```

- 修改高度每行/组头/组尾部的高度

  ```objc
  // Variable height support
  - (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath;
  - (CGFloat)tableView:(UITableView *)tableView heightForHeaderInSection:(NSInteger)section;
  - (CGFloat)tableView:(UITableView *)tableView heightForFooterInSection:(NSInteger)section;
  ```

- 设置估算高度

  ```objc
  //使用所估计的高度的方法来快速计算猜到值，这将允许对表中的快速加载时间。
  //如果这些方法的实施，上述-tableView：heightForXXX 将被推迟到的意见已准备好进行显示，这样更加优先的逻辑可以放在那里。
  - (CGFloat)tableView:(UITableView *)tableView estimatedHeightForRowAtIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(7_0);
  - (CGFloat)tableView:(UITableView *)tableView estimatedHeightForHeaderInSection:(NSInteger)section NS_AVAILABLE_IOS(7_0);
  - (CGFloat)tableView:(UITableView *)tableView estimatedHeightForFooterInSection:(NSInteger)section NS_AVAILABLE_IOS(7_0);
  ```

- 设置组头/组尾部的View 

  ```objc
  //组头和组脚视图。你如果同时提供标题和视图, 则视图是优于标题显示;
  // Section header & footer information. Views are preferred over title should you decide to provide both
  - (nullable UIView *)tableView:(UITableView *)tableView viewForHeaderInSection:(NSInteger)section;   // custom view for header. will be adjusted to default or specified header height
  - (nullable UIView *)tableView:(UITableView *)tableView viewForFooterInSection:(NSInteger)section;   // custom view for footer. will be adjusted to default or specified footer height

  // Accessories (disclosures). 
  // 附件类型一行索引路径
  - (UITableViewCellAccessoryType)tableView:(UITableView *)tableView accessoryTypeForRowWithIndexPath:(NSIndexPath *)indexPath NS_DEPRECATED_IOS(2_0, 3_0) __TVOS_PROHIBITED;
  // 附件按钮横置以一行索引路径
  - (void)tableView:(UITableView *)tableView accessoryButtonTappedForRowWithIndexPath:(NSIndexPath *)indexPath;
  ```

- 选中 tableView 某行时调用的方法

  ```objc
  // Selection
  // -tableView:shouldHighlightRowAtIndexPath: is called when a touch comes down on a row. 
  // Returning NO to that message halts the selection process and does not cause the currently selected row to lose its selected look while the touch is down.
  - (BOOL)tableView:(UITableView *)tableView shouldHighlightRowAtIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(6_0);
  - (void)tableView:(UITableView *)tableView didHighlightRowAtIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(6_0);
  - (void)tableView:(UITableView *)tableView didUnhighlightRowAtIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(6_0);

  // Called before the user changes the selection. Return a new indexPath, or nil, to change the proposed selection.
  - (nullable NSIndexPath *)tableView:(UITableView *)tableView willSelectRowAtIndexPath:(NSIndexPath *)indexPath;
  - (nullable NSIndexPath *)tableView:(UITableView *)tableView willDeselectRowAtIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(3_0);
  // Called after the user changes the selection.
  - (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath;
  - (void)tableView:(UITableView *)tableView didDeselectRowAtIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(3_0);
  ```

- 编辑时调用的方法

  ```objc
  // Editing
  //允许editingStyle定制了位于“indexPath”特定的 Cell 。如果不执行，所有可编辑的单元将具有UITableViewCellEditingStyleDelete为它们设置，当表编辑属性设置为YES。
  // Allows customization of the editingStyle for a particular cell located at 'indexPath'. If not implemented, all editable cells will have UITableViewCellEditingStyleDelete set for them when the table has editing property set to YES.
  - (UITableViewCellEditingStyle)tableView:(UITableView *)tableView editingStyleForRowAtIndexPath:(NSIndexPath *)indexPath;
  - (nullable NSString *)tableView:(UITableView *)tableView titleForDeleteConfirmationButtonForRowAtIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED;
  - (nullable NSArray<UITableViewRowAction *> *)tableView:(UITableView *)tableView editActionsForRowAtIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED; // supercedes -tableView:titleForDeleteConfirmationButtonForRowAtIndexPath: if return value is non-nil

  //控制是否背景在编辑缩进。如果没有执行，默认是YES。这是不相关的下面的缩进级别。此方法仅适用于组合风格的表视图。
  // Controls whether the background is indented while editing.  If not implemented, the default is YES.  This is unrelated to the indentation level below.  This method only applies to grouped style table views.
  - (BOOL)tableView:(UITableView *)tableView shouldIndentWhileEditingRowAtIndexPath:(NSIndexPath *)indexPath;

  //在开始/结束方法每当'编辑'属性被自动表改变（允许插入/删除/移动）。这是通过一个滑动激活单行完成
  // The willBegin/didEnd methods are called whenever the 'editing' property is automatically changed by the table (allowing insert/delete/move). This is done by a swipe activating a single row
  - (void)tableView:(UITableView*)tableView willBeginEditingRowAtIndexPath:(NSIndexPath *)indexPath __TVOS_PROHIBITED;
  - (void)tableView:(UITableView*)tableView didEndEditingRowAtIndexPath:(NSIndexPath *)indexPath __TVOS_PROHIBITED;
  ```

- 移动/重排序

  ```objc
  // Moving/reordering
  // 允许目标行的特定行的定制，因为它是被移动/重新排序
  // Allows customization of the target row for a particular row as it is being moved/reordered
  - (NSIndexPath *)tableView:(UITableView *)tableView targetIndexPathForMoveFromRowAtIndexPath:(NSIndexPath *)sourceIndexPath toProposedIndexPath:(NSIndexPath *)proposedDestinationIndexPath;
  ```

- 缩进

  ```objc
  // Indentation
  //返回行缩进“深度”的层次结构
  - (NSInteger)tableView:(UITableView *)tableView indentationLevelForRowAtIndexPath:(NSIndexPath *)indexPath; // return 'depth' of row for hierarchies
  ```

- 复制粘贴

  ```objc
  // 复制粘贴 这上个方法都必须有代理实现
  // Copy/Paste.  All three methods must be implemented by the delegate.
  - (BOOL)tableView:(UITableView *)tableView shouldShowMenuForRowAtIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(5_0);
  - (BOOL)tableView:(UITableView *)tableView canPerformAction:(SEL)action forRowAtIndexPath:(NSIndexPath *)indexPath withSender:(nullable id)sender NS_AVAILABLE_IOS(5_0);
  - (void)tableView:(UITableView *)tableView performAction:(SEL)action forRowAtIndexPath:(NSIndexPath *)indexPath withSender:(nullable id)sender NS_AVAILABLE_IOS(5_0);
  ```

- 焦点

  ```objc
  // Focus
  - (BOOL)tableView:(UITableView *)tableView canFocusRowAtIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(9_0);
  - (BOOL)tableView:(UITableView *)tableView shouldUpdateFocusInContext:(UITableViewFocusUpdateContext *)context NS_AVAILABLE_IOS(9_0);
  - (void)tableView:(UITableView *)tableView didUpdateFocusInContext:(UITableViewFocusUpdateContext *)context withAnimationCoordinator:(UIFocusAnimationCoordinator *)coordinator NS_AVAILABLE_IOS(9_0);
  - (nullable NSIndexPath *)indexPathForPreferredFocusedViewInTableView:(UITableView *)tableView NS_AVAILABLE_IOS(9_0);
  ```


---

## <a id="UITableView的性能优化"></a>5. UITableView的性能优化

- **性能优化的思路**
    -  iOS 设备的内存有限，如果用UITableView显示成千上万条数据，就需要成千上万个UITableViewCell对象的话，那将会耗尽iOS设备的内存。要解决该问题，需要重用UITableViewCell对象


- **性能优化的具体实现**
	- 当滚动列表时，部分UITableViewCell会移出窗口，UITableView会将窗口外的UITableViewCell放入一个对象池中，等待重用
	- 当UITableView要求dataSource返回UITableViewCell时，dataSource会先查看这个对象池，如果池中有未使用的UITableViewCell，dataSource会用新的数据配置这个UITableViewCell，然后返回给UITableView，重新显示到窗口中，从而避免创建新对象


- **传统写法（一般写法）**
  ```objc
  /** 每当一个cell要进入视野范围就会调用这个方法 */
  - (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
  {
      // 1.定义一个重用标识
      static NSString *ID = @"wine";
      // 2.去缓存池取可循环利用的cell
      UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:ID];

      // 3.缓存池如果没有可循环利用的cell,自己创建
      if (cell == nil) {
          cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:ID];
          // 建议:所有cell都一样的设置,写在这个大括号中;所有cell不都一样的设置写在外面
         cell.backgroundColor = [UIColor redColor];

      }
      // 4.设置数据
      cell.textLabel.text = [NSString stringWithFormat:@"第%zd行数据",indexPath.row];

      return cell;
  }
  ```


- **注册写法**(经常用于自定义 UITableViewCell 中)

  ```objc
  NSString *ID = @"wine";

  - (void)viewDidLoad {
      [super viewDidLoad];

      // 注册ID 这个标识对应的cell类型为UITableViewCell 
      // 注册有三种方法: 类名注册/ xib 注册/ storyboard 注册
      [self.tableView registerClass:[UITableViewCell class] forCellReuseIdentifier:ID];
  }

  - (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
  {
      // 1.先去缓存池中查找可循环利用的cell
      UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:ID];

      // 2.设置数据
      cell.textLabel.text = [NSString stringWithFormat:@"%zd行的数据", indexPath.row];

      return cell;
  }
  ```


---
## <a id="UITableView的索引条"></a>6. UITableView的索引条

- **设置右边索引文字的颜色**

  ```objc
  self.tableView.sectionIndexColor = [UIColor redColor];
  ```

- **设置右边索引文字的背景色**

  ```objc
  self.tableView.sectionIndexBackgroundColor = [UIColor blackColor];
  ```
	
- **返回每一组的索引标题**

  ```objc
  - (NSArray *)sectionIndexTitlesForTableView:(UITableView *)tableView
  ```


---

- **例子**

  ```objc
  @interface ViewController ()

  @property (nonatomic, strong) NSArray *carGroups;

  @end

  @implementation ViewController

  #pragma  mark - carGroups
  /**
   *  懒加载思想，重写 carGroups 的 getter 方法
   */
  - (NSArray *)carGroups{

      if (!_carGroups) {

          //        1. 加载 plist 文件的数据
          //        1.1 获取包文件
          NSBundle *bundle = [NSBundle mainBundle];
          //        1.2 获取文件全路径
          NSString *path = [bundle pathForResource:@"cars" ofType:@"plist"];
          //        1.3 加载 plist 文件的数据到数组中
          NSArray  *arrayDictionary = [NSArray arrayWithObject:path];

          //        2. 数组转模型
          //        2.1 新建一个可变的临时数组
          NSMutableArray *tempMutableArray = [[NSMutableArray alloc]init];
          for (NSDictionary *dict in arrayDictionary) {
              //            2.2 通过 kvc 快速字典转模型
              //            2.2.1 定义个临时的车组模型，接收字典转模型后的模型
              CDHCarGroup *carGroup = [CDHCarGroup carGroupWithDictionary:dict];
              //            2.2.2 将模型添加入到可变数组中
              [tempMutableArray addObject:carGroup];
          }
          //        3. 将数组赋值给 carGroups 属性
          _carGroups = tempMutableArray;
      }
      //    4. 返回 carGroups 车组数组类型的属性
      return _carGroups;
  }

  - (void)viewDidLoad {
      [super viewDidLoad];

  }

  /**
   *  隐藏状态栏(隐藏手机最上面的状态栏电池电量、WiFi、时间显示等状态)
   */
  - (BOOL)prefersStatusBarHidden
  {
      return YES;
  }

  #pragma mark - 数据源方法
  /**
   *  设置分组数
   */
  - (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView{
      return _carGroups.count;   
  }
  /**
   *  设置每组的行数,
   *  section 参数是组号
   */
  - (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section{
  //    1. 先得到是属于哪一组的
      CDHCarGroup *Group = self.carGroups[section];
  //    2. 根据组数在返回该组的行数
      return Group.cars.count;
  }

  /**
   *  创建 UITableViewCell 或者 子类控件并返回该对象
   */
  - (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath{

  //    1. 定义重用标示
      static NSString *ID = @"car";
  //    2. 访问缓存池
      UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:ID];

  //    3. 缓存池没有可用的 cell ,就自己创建
      if (cell == nil) {
  //        4. 创建一个 cell
          cell = [[UITableViewCell alloc]initWithStyle:UITableViewCellStyleDefault reuseIdentifier:ID];

      }
  //    5. 设置数据
  //    5.1 获取对应组号
      CDHCarGroup *group = self.carGroups[indexPath.section];
  //    5.2 获取行号
      CDHCar *car  =  group.cars[indexPath.row];

  //    5.3 设置 cell 中的 images
      cell.imageView.image = [UIImage imageNamed:car.icon];
  //    5.4 设置 cell 中的 text
      cell.textLabel.text = car.name;

      return cell;

  }

  /**
   *  设置每组的标题，并返回标题对象
   */
  - (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section {

  //    取出第 section 组的对应的模型
      CDHCarGroup *group = self.carGroups[section];

      return group.title;

  }

  /**
   *  告诉tableView显示的索引文字
   */
  - (NSArray<NSString *> *)sectionIndexTitlesForTableView:(UITableView *)tableView{
      // 抽取self.carGroups这个数组中每一个元素(XMGCarGroup对象)的title属性的值,并且放在一个新的数组中返回
      return [self.carGroups valueForKeyPath:@"title"];
  }

  @end
  ```