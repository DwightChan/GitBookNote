# 控制器view生命周期

- 控制器View的生命周期方法:只要是控制器的生命周期方法,都是以view开头.

- **ARC的生命周期**
    - `viewDidLoad`->`viewWillAppear`->`viewWillLayoutSubviews`->`viewDidLayoutSubviews`->`viewDidAppear`->`viewWillDisappear`->`viewDidDisappear`

- **非ARC的生命周期**
    - `viewDidLoad`->`viewWillAppear`->`viewDidLayoutSubviews`->`viewDidLayoutSubviews`->`viewDidAppear`->`viewWillDisappear`->`viewDidDisappear`->`接收到内存警告`->`viewWillUnload`->`释放View`->`viewDidUnload`

```objc
//控制器View加载完成时调用
- (void)viewDidLoad {
    [super viewDidLoad];
     
}

//控制器的View显示完成时调用
-(void)viewDidAppear:(BOOL)animated{
    [super viewDidAppear:animated];

}

//控制器的View即将显示的时候调用
-(void)viewWillAppear:(BOOL)animated{
    [super viewWillAppear:animated];

}

//控制器的View完全消失的时候调用
-(void)viewDidDisappear:(BOOL)animated{
    [super viewDidDisappear:animated];

}

//控制器的View即将消失的时候调用.
-(void)viewWillDisappear:(BOOL)animated{
    [super viewWillDisappear:animated];

}

//布局控制器View的子控件完成时调用
-(void)viewDidLayoutSubviews{
    [super viewDidLayoutSubviews];

}

//将要布局控制器的View里面子控件的时候就会调用.
-(void)viewWillLayoutSubviews{
    [super viewWillLayoutSubviews];

}

//ARC的生命周期

//viewDidLoad->viewWillAppear->viewWillLayoutSubviews->viewDidLayoutSubviews
//->viewDidAppear->viewWillDisappear->viewDidDisappear

//在 MRC当中.
//当前控制器的View即将被销毁的时候会调用
-(void)viewWillUnload{
    [super viewWillUnload];
}

//当前控制器的View被销毁的时候会调用
-(void)viewDidUnload{
    [super viewDidUnload];
    // 清空界面上的数据.
     self.dataList = nil;
}

//在 MRC 中
//viewDidLoad->viewWillAppear->viewDidLayoutSubviews->viewDidLayoutSubviews
//->viewDidAppear->viewWillDisappear->viewDidDisappear->接收到内存警告
//->viewWillUnload->释放View->viewDidUnload
```


---
<br/>