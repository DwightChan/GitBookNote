# 自定义城市键盘(初始化文字处理)

```objc
//当光标点击文本框的时候,让文本框的文字为第一个自定义键盘选中的文字.

//所以坚听文本框架的开始编辑的代理
//开始编辑时调用,(弹出键盘)became first responder
- (void)textFieldDidBeginEditing:(UITextField *)textField{

}
//在这个代理方法当中做事情.

//每一个文本框当中都提供一个初始化的方法.当在控制器当中调用这个初始化的方法.
//方法的目的就是让开始编辑选中第一列的第一行.
- (void)initWithText;

//国旗键盘初始化方法实现:
- (void)initWithText{
    [self pickerView:nil didSelectRow:0 inComponent:0];
}

//日期键盘初始化方法实现:
- (void)initWithText{
    [self dateChange:self.pick];
}

//城市键盘初始化方法实现:
- (void)initWithText{
    [self pickerView:self.pick didSelectRow:0 inComponent:0];
}

//把方法的参数改成国旗,或者日期,或者城市的类型,改的一个目的是让它能够找到initWithText方法.
//传进来的参数真实类型是什么类型, 它就会去调用它真实类型的方法.
//如果传进来的键盘类型为日期键盘,它就会调用日期的初始化方法.如果真实类型为城市,它就会去调用城市的初始化方法.
- (void)textFieldDidBeginEditing:( FlagField *)textField{
     //会去找它真实类型的方法
     [textField initWithText];
}
```