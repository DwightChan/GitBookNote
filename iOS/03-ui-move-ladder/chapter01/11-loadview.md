# 11-loadView


## 1. 一些基本的概念

- **loadView作用**:控制器会调用该方法去创建控制器的View.


- **View 的加载流程**
    1. 先去判断当前控制器是不是从StoryBoard当中加载的,如果是,那么它就会从StoryBoard当中加载控制器的View.
    2. 如果不是从StoryBoard当中加载的, 那么它还会判断是不是从Xib当中创建的控制器.如果是,那么它就会从xib加载控制器的View.
    3. 如果也不是从Xib加载的控制器.那么它就会创建一个空(透明)的UIView.设为当前控制器的View.
   **注意：**这里指的空（透明）的 UIView 是指 view 的背景颜色


- **什么时候调用**:当第一次使用控制器的View的时候
- **开发中loadView使用场景**:自定义控制器的View.
    - 设置控制器的View直接是一个UIImageView. 或者是一个UIWebView时候,可以直接让控制器一开始创建的时候就是它.这样做的好处少创建了一个UIView.


- ** 注意:**
    1. 一旦重写了loadView,表示需要自己创建控制器的View.(storyboard 和 xib 加载的都失效)
    2. 如果控制器的View还没有赋值,就不能调用控制器View的get方法.会造成死循环.因为控制器View的get方法底层会调用loadView方法.

```objc
// 懒加载控制器的View.
// 控制器View的get方法
//- (UIView *)view{
//    if (_view == nil) {
//        [self loadView];
//        [self viewDidLoad];
//    }
//    return _view;
//}
```

```objc
// 重写LoadView,自定义控制器的View.
-(void)loadView{
    XMGView *redView =  [[XMGView alloc] initWithFrame:[UIScreen mainScreen].bounds];
    redView.backgroundColor = [UIColor redColor];
    self.view = redView;
}
```


```objc
- (void)viewDidLoad; // Called after the view has been loaded. For view controllers created in code, this is after -loadView. For view controllers unarchived from a nib, this is after the view is set.
```


##2.loadView方法中调用，验证默认加载视图的方式

###2.1 没有重写 loadView 方法

####2.1.1 使用纯代码加载控制器的 view

- 先将 info.plist 文件中的 Key : Main storyboard file base name 对应的 Value :Main 删除
- 在 AppDelegate.m 文件中的 启动加载完成就会调用的方法中手动加载控制器以及控制器的 View

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // 在这里手动创建窗口、设置窗口的根控制器、显示窗口
    return YES;
}
```



####2.1.2 通过 storyboard 加载控制器的 View 

-  **先加载指定的StoryBoard**.
-  纯代码加载StoryBoard必须要有指定名字才能加载,就算StoryBoard与控制器同名,也没有别的方法,
-  即是不能直接使用 alloc / init 加载

```objc
// 错误代码
UIStoryboard *storyBoard = [[UIStoryboard alloc]init];
// 正确写法
UIStoryboard *storyBoard = [UIStoryboard storyboardWithName:@"Main" bundle:nil];
//    UIStoryboard *storyBoard = [UIStoryboard storyboardWithName:@"MyStoryBoard" bundle:nil];
```

- **1.加载箭头所指向的控制器.**

```objc
UIViewController *vc = [storyBoard instantiateInitialViewController];
```

- **2.加载指定标识的控制器.**

```objc
UIViewController *vc = [storyBoard instantiateViewControllerWithIdentifier:@"grayView"];
```

####2.1.3 通过 xib 加载控制器view的流程


- **手动创建窗口；**
- **设置窗口的根控制器**   
    - 通过 xib 描述控制器的 view   
    - 在 xib 中做两件事     
        >第一步，告诉 xib，描述的是哪个控制器    
        >第二步，告诉 xib 使用其中哪个 View 来描述控制器的 view
        
- **显示窗口**

    - 直接使用 alloc/init 加载控制器默认会调用 initWithNibName: 这个方法加载控制器的 View
    - 即是使用initWithNibName: 方法加载控制器的view：


- **加载 xib 的优先顺序**
    - 如果指定了名称,那么它就会加载指定名称的xib
    - 如果没有指定名称为nil,那么它会默认去加载跟它同名的Xib(RootViewController.xib)
    - 如果没有跟它跟同名的xib,那么它还会去加载跟它相同名称去掉Controller的Xib(RootView.xib)
    - 如果以上三种都没有则会创建一个空白（透明色）的 View 作为控制器的 View (如果看到黑色则可能是窗口的颜色)

```
注意： 在 Xcode 7.0 以前这个优先级顺序是不一样的：（同Xcode7.0 之后中的2和3 顺序调换）
1. 如果指定了名称,那么它就会加载指定名称的xib
2. 如果没有跟它跟同名的xib,那么它还会去加载跟它相同名称去掉Controller的Xib(RootView.xib)
3. 如果没有指定名称为nil,那么它会默认去加载跟它同名的Xib(RootViewController.xib)
4. 如果以上三种都没有则会创建一个空白（透明色）的 View 作为控制器的 View
```


###2.2 重写 loadView 方法

####2.2.1 使用纯代码加载控制器的 view

- 先将 info.plist 文件中的 Key : Main storyboard file base name 对应的 Value :Main 删除
- 在 AppDelegate.m 文件中的 启动加载完成就会调用的方法中
- **在loadView中创建自己的view可以不给frame，系统会自动设置控制器view的尺寸。**

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // 在这里手动创建窗口、设置窗口的根控制器、显示窗口
    return YES;
}
```



####2.2.2 通过 storyboard 加载控制器的 View 



-  **先加载指定的StoryBoard.**

```objc
UIStoryboard *storyBoard = [UIStoryboard storyboardWithName:@"Main" bundle:nil];
//    UIStoryboard *storyBoard = [UIStoryboard storyboardWithName:@"MyStoryBoard" bundle:nil];
```

- **1.加载箭头所指向的控制器.并重写 loadView 方法**


```objc
// 加载storyboard 当前箭头中指向的控制器
UIViewController *vc = [storyBoard instantiateInitialViewController];
```

- **2.加载指定标识的控制器.并重写 loadView 方法**

```objc
UIViewController *vc = [storyBoard instantiateViewControllerWithIdentifier:@"blueCv"];
```

- **以上两种方式加载 storyboard 控制器中的 View 如果重写loadView 方法之后的结果是一样的,如下:**

```objc
// 重写 loadview 方法
- (void)loadView{
//    这里没有写一条语句,则是会自己创建一个空的 View
//    (空的则是指颜色是透明的,如果看到黑色是窗口的颜色)
}
```

```objc
// 重写 loadview 方法
- (void)loadView{
//    这里如果写了下面一句话,相当于没用重写 loadView 方法
//    也还是会加载原来storyboard 里面控制中的 View 
//    (有设置颜色则显示对应颜色)
    [super loadView];
}
```

```objc
// 重写 loadview 方法
- (void)loadView{
    UIView *redView = [[UIView alloc]init];
    redView.backgroundColor = [UIColor redColor];
    self.view = redView;
//    只要重写了这个方法并在创建了一个新的 view ,并给这个 view 相应的颜色,则就是新创建的 view 并以对应的颜色显示
}
```

```objc
// 重写 loadview 方法
- (void)loadView{
    [super loadView];
    UIView *blueView = [[UIView alloc]init];
    blueView.backgroundColor = [UIColor blueColor];
    self.view = blueView;
//    如果要自己创建新的 View ,就没必要在 loadView 方法的前面写[super loadView];了
//    注意,这里的位置,如果 [super loadView];方法在 self.view = blueView 之后,则还是会加载 storyboard 中的 View
}
```

---

####2.2.3 通过 xib 加载控制器view的流程

- **通过 xib 加载如果有指定名字(结果也就个 storyboard 的结果一样)**

```objc
CDHViewController *vc = [[CDHViewController alloc]initWithNibName:@"CDH" bundle:nil];
```

```objc
// 重写 loadview 方法
- (void)loadView{
//    这里没有写一条语句,则是会自己创建一个空的 View
//    (空的则是指颜色是透明的,如果看到黑色是窗口的颜色)
}
```

```objc
// 重写 loadview 方法
- (void)loadView{
     [super loadView];
//    这里如果写了上面一句话,相当于没用重写 loadView 方法
//    也还是会加载原来指定名字 xib 里面控制中的 View 
//    (有设置颜色则显示对应颜色)

}
```

```objc
// 重写 loadview 方法
- (void)loadView{
    UIView *redView = [[UIView alloc]init];
    redView.backgroundColor = [UIColor redColor];
    self.view = redView;
//    只要重写了这个方法并在创建了一个新的 view ,并给这个 view 相应的颜色,则就是新创建的 view 并以对应的颜色显示
}
```

```objc
// 重写 loadview 方法
- (void)loadView{
    [super loadView];
    UIView *blueView = [[UIView alloc]init];
    blueView.backgroundColor = [UIColor blueColor];
    self.view = blueView;
//    如果要自己创建新的 View ,就没必要在 loadView 方法的前面写[super loadView];了
//    注意,这里的位置,如果 [super loadView];方法在 self.view = blueView 之后,则还是会加载 storyboard 中的 View
}
```


- **通过 xib 加载没如果没有指定名字**

```objc
CDHViewController *vc = [[CDHViewController alloc]init];
```

- **只要重写了 loadView 方法,无论在该方法中有没有写`[super loadView];`都不会再加载任何 xib 中的 View**

```objc
// 重写 loadview 方法
- (void)loadView{
//    这里没有写一条语句,则是会自己创建一个空的 View
//    (空的则是指颜色是透明的,如果看到黑色是窗口的颜色)
}
```

```objc
// 重写 loadview 方法
- (void)loadView{
    [super loadView];
//    写了这条语句,也还是是会自己创建一个空的 View
//    (空的则是指颜色是透明的,如果看到黑色是窗口的颜色)
}
```

```objc
// 重写 loadview 方法
- (void)loadView{
    UIView *redView = [[UIView alloc]init];
    redView.backgroundColor = [UIColor redColor];
    self.view = redView;
//    只要重写了这个方法并在创建了一个新的 view ,并给这个 view 相应的颜色,
//    则就是新创建的 view 并以对应的颜色显示
}
```

```objc
// 重写 loadview 方法
- (void)loadView{
    [super loadView]; // 这里创建了个空的 View
    UIView *blueView = [[UIView alloc]init];
    blueView.backgroundColor = [UIColor blueColor];
    self.view = blueView;
//    如果要自己创建新的 View ,就没必要在 loadView 方法的前面写[super loadView];了
//    注意,这里的位置,如果 [super loadView];方法在 self.view = blueView 之后,
//    则最后结果只会是一个空的 View
}
```


