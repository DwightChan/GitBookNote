# 父类特定的方法

##1. 构造方法
- **注意:子类如果重写了父类的特定构造方法, 那么必须使用super调用父类的特定构造方法**
- **`Designated initializer` : 特定构造方法(方法声明后面带有`NS_DESIGNATED_INITIALIZER`)**

  ```objc
  /*
   Designated initializer : 特定构造方法(方法声明后面带有NS_DESIGNATED_INITIALIZER)

   Designated initializer missing a 'super' call to a designated initializer of the super class
   注意:子类如果重写了父类的特定构造方法, 那么必须使用super调用父类的特定构造方法
   */

  - (instancetype)initWithFrame:(CGRect)frame
  {
      if (self = [super initWithFrame:frame]) {
          self.titleLabel.font = [UIFont systemFontOfSize:16];
          // 文字颜色
          [self setTitleColor:[UIColor darkGrayColor] forState:UIControlStateNormal];
          [self setTitleColor:[UIColor redColor] forState:UIControlStateSelected];
      }
      return self;
  }
  ```

##2. 其他特定的方法

- **其他特定方法(方法声明后面带有`NS_REQUIRES_SUPER`)**

  ```objc
  //- 父类的方法
  - (void)run NS_REQUIRES_SUPER;
  //- 子类重写父类的方法
  - (void)run{
      [super run];
       // 如果没有调父类的方法会报警告, 
       // 再如果父类的方法做了些特定的操作, 
       // 而子类没有使用则会可导致有莫名其妙的错误.
  }
  ```