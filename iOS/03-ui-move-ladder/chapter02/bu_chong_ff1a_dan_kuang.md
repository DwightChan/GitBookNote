# 补充：弹框(比较前后两种)



##1. iOS8 之前的弹窗框（是 View）

- 是个 View 视图
- 需要代理，代理遵循协议，实现代理方法` <UIAlertViewDelegate>`

```objc
- (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{

//     iOS8 之前的弹窗框（是 View）
//     1. 创建弹框
//        initWithTitle:标题
//        message：信息
//        delegate:代理
//        cancelButtonTitle：取消按钮的文字
//        otherButtonTitles：其他按钮标题（用逗号隔开）
    UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:@"提示" message:@"你妈叫你回家吃饭了！" delegate:self cancelButtonTitle:@"取消" otherButtonTitles:@"确定",@"大撒比",@"草泥马", nil];
    
    alertView.title = @"温馨提示！";
    alertView.message = @"广州多云转阴大，是有雷阵雨，黄色预警";
    [alertView addButtonWithTitle:@"新闻联播"];
    [alertView buttonTitleAtIndex:0];
    [alertView dismissWithClickedButtonIndex:1 animated:YES];
    alertView.alertViewStyle = UIAlertViewStylePlainTextInput;


//     显示
    [alertView show];
}
```

```objc
// 代理方法；例如：
- (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex{
    NSLog(@"我被点击了");
}
```


---


##2. ISO8 之后的弹窗框（controller）
- 自身就是个控制器，不需要代理

```objc
- (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{

    //    ISO8 之后的弹窗框（controller）
    
    // 1. 创建弹框
    UIAlertController *alertVc = [UIAlertController alertControllerWithTitle:@"tip" message:@"你妈叫你回去吃饭了，傻逼！" preferredStyle:UIAlertControllerStyleAlert];
    /*
     UIAlertControllerStyleActionSheet = 0, 底下弹窗
     UIAlertControllerStyleAlert            中间弹窗
     */
    
    // 2. 添加按钮
    //    handler: 点击按钮后做的事情
    //    style: 添加的按钮类型
    //    （注意：每个弹窗控制器每种按钮类型，只能有一个，即是有三种按钮类型也就最多只能添加三个按钮，每种各一个）
    /* 
     枚举值
     UIAlertActionStyleDefault = 0,
     UIAlertActionStyleCancel,
     UIAlertActionStyleDestructive
     */
    UIAlertAction *cancleBtn = [UIAlertAction actionWithTitle:@"取消" style:UIAlertActionStyleCancel handler:^(UIAlertAction * _Nonnull action) {
        NSLog(@"取消按钮");
    }];
    
    UIAlertAction *defaultBtn = [UIAlertAction actionWithTitle:@"默认" style:UIAlertActionStyleDefault handler:^(UIAlertAction * _Nonnull action) {
        NSLog(@"默认型按钮");
    }];
    UIAlertAction *destructiveBtn = [UIAlertAction actionWithTitle:@"警告" style:UIAlertActionStyleDestructive handler:^(UIAlertAction * _Nonnull action) {
        NSLog(@"毁灭性按钮");
    }];
    
    // 3. 添加按钮
    [alertVc addAction:cancleBtn];
    [alertVc addAction:defaultBtn];
    [alertVc addAction:destructiveBtn];
    /*
    注意：这三种类型的按钮添加到 alertVc弹窗控制器中不论先后顺序是如何，排列顺序都是根据优先级排列（只有两个按钮，则左右各一个，三个按钮则竖排上中下）
    优先级：
     UIAlertActionStyleCancel > UIAlertActionStyleDefault == UIAlertActionStyleDestructive
    
     UIAlertActionStyleCancel 类型的 cancleBtn 总是放在左边 或则最下边一个位置
     UIAlertActionStyleDefault == UIAlertActionStyleDestructive
     另外两种优先级相同则根据排列添加的先后顺序，从左到右，或则从上到下；
     */
    
    // 4. 显示
    [self presentViewController:alertVc animated:YES completion:nil];
}
```