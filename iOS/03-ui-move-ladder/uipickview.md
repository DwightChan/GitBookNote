# UIPickView
<br/>
##本节知识点
1. UIPickView的基本使用
2. UIPickView简单Demo



---
<br/>

##1. UIPickView的基本使用

- **UIPickView和TableView一样,想要展示数据也要设置数据源和代理**


- **设置数据源**

  ```objc
  self.pickView.dataSource = self;
  ```

- **设置代理**

  ```objc
  self.pickView.delegate = self;
  ```

- **遵守数据源,代理协议:**

  ```objc
  @interface ViewController ()<UIPickerViewDataSource,UIPickerViewDelegate>
  @property (weak, nonatomic) IBOutlet UIPickerView *pickView;
  @end
  ```

- **实现数据源代理方法:**

- 总共有多少列

  ```objc
  - (NSInteger)numberOfComponentsInPickerView:(UIPickerView *)pickerView{
      return 3;
  }
  ```

- 第component列有多少行.

  ```objc
  - (NSInteger)pickerView:(UIPickerView *)pickerView numberOfRowsInComponent:(NSInteger)component{
      return 4;
  }
  ```

- 返回每一列的宽度

  ```objc
  - (CGFloat)pickerView:(UIPickerView *)pickerView widthForComponent:(NSInteger)component{
  }
  ```

- 返回第一列的高度

  ```objc
  - (CGFloat)pickerView:(UIPickerView *)pickerView rowHeightForComponent:(NSInteger)component{
      return 50;
  }
  ```

- 返回每一行的标题

  ```objc
  - (nullable NSString *)pickerView:(UIPickerView *)pickerView titleForRow:(NSInteger)row forComponent:(NSInteger)component{
      return @"gaowei";
  }
  ```

- 返回每一行的视图UIView

  ```objc
  - (UIView *)pickerView:(UIPickerView *)pickerView viewForRow:(NSInteger)row forComponent:(NSInteger)component reusingView:(nullable UIView *)view{

      UIButton *btn = [UIButton buttonWithType:UIButtonTypeContactAdd];
      return btn;
  }
  ```

- 展示带有属性的内容(文字的颜色,大小...)

  ```objc
  - (nullable NSAttributedString *)pickerView:(UIPickerView *)pickerView attributedTitleForRow:(NSInteger)row forComponent:(NSInteger)component{

  }
  ```

- 选中某一行的时候调用

  ```objc
  - (void)pickerView:(UIPickerView *)pickerView didSelectRow:(NSInteger)row inComponent:(NSInteger)component{
      NSLog(@"component===%ld    row===%ld",component,row);
  }
  ```

---
<br/>
##2. UIPickView简单Demo

- 定义相应的属性

  ```objc
  #import "ViewController.h"

  @interface ViewController ()<UIPickerViewDataSource,UIPickerViewDelegate>
  //展示数据的pickView
  @property (weak, nonatomic) IBOutlet UIPickerView *pickView;

  //数组当中有3个小数组, 每一个小数组代表一列.每一列小数组的个数代表这一列有多少行.
  @property(nonatomic,strong) NSArray *foodArray;
  //显示当前选中的食物
  @property (weak, nonatomic) IBOutlet UILabel *foodLabel;

  @end
  ```



- 懒加载数据

  ![png](../images/UIPickView/UIPickerView-food图解.png)

  ```objc
  -(NSArray *)foodArray{

      if ( !_foodArray ) {
          //获取Plist文件的路径
          NSString *filePath = [[NSBundle mainBundle] pathForResource:@"foods.plist" ofType:nil];
          //从Plist文件当中加载数组.
          _foodArray = [NSArray arrayWithContentsOfFile:filePath];

      }
      return _foodArray;
  }
  ```

- 设置数据源和代理

  ```objc
  - (void)viewDidLoad {
      [super viewDidLoad];
      //设置数据源
      self.pickView.dataSource = self;
      //设置代理
      self.pickView.delegate = self;
  }
  ```

- 实现数据源方法

  ```objc
  //总共有多少列
  - (NSInteger)numberOfComponentsInPickerView:(UIPickerView *)pickerView{
      // 数组当中有几个元素, 就展示多少列.每一个元素代表一列,
      return self.foodArray.count;
  }
  ```
  ```objc
  //第component列有多少行.
  - (NSInteger)pickerView:(UIPickerView *)pickerView numberOfRowsInComponent:(NSInteger)component{
      //取出当前所在的列.每一列都是一个数组.
      NSArray *array = self.foodArray[component];
      //返回每一组当中, 每一个小数组的数个, 也就是这一组里面有多少行.
      return array.count;
  }
  ```
  ```objc
  //返回每一行的标题
  - (nullable NSString *)pickerView:(UIPickerView *)pickerView titleForRow:(NSInteger)row forComponent:(NSInteger)component{
      //取出当前所在的列.每一列都是一个数组.
      NSArray *componentArray = self.foodArray[component];
      //返回小数组当中每一个元素
      return componentArray[row];
  }
  ```

- 实现代理方法

  ```objc
  //点击了哪一列的哪一行
  - (void)pickerView:(UIPickerView *)pickerView didSelectRow:(NSInteger)row inComponent:(NSInteger)component{
      NSString *food = self.foodArray[component][row];
      self.foodLabel.text = food;
  }
  ```

---
<br/>

