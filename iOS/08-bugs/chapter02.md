# Chapter02

##动漫的使用注意

- **前后分别执行不同动漫动作的写法注意点**

    - 不能直接使用两个动漫连续使用
    - 比如:

```objc
// 比如01:
// 不能直接使用两个动漫连续使用,(同级并联)
// 如下最终结果只会执行后面一个动画;
[UIView animateWithDuration:animateTime animations:^{
    self.mainV.frame = [UIScreen mainScreen].bounds;
}];
[UIView animateWithDuration:animateTime animations:^{
    self.mainV.frame = CGRectMake(100, 100, 100, 100);
}];
```

```objc
// 比如02:
// 这里就算 if 语句能够进来也不会执行 if 语句里面的动漫(动漫里面的语句可能不执行,但不会有动漫)
// 是指定到 if 里面的动漫的时候回直接跳 if 外面的语句执行完外面的动漫之后
// 会在调回 if 中动漫的 completion 里面执行完毕会执行的语句(这里也就是会执行就 NSLog 打印);

if (self.mainV.frame.origin.x != 0){
    [UIView animateWithDuration:animateTime animations:^{
        self.mainV.frame = [UIScreen mainScreen].bounds;
    }completion:^(BOOL finished) {
        NSLog(@"%s",__func__);
    }];
}
[UIView animateWithDuration:animateTime animations:^{
    self.mainV.frame = CGRectMake(100, 100, 100, 100);
}];
```

- **如果前后两个不同的动漫都要执行,则必须嵌套**


```objc
// 正确写法
if (self.mainV.frame.origin.x != 0){
    // 如果前后两个不同的动漫都要执行,则必须嵌套
    [UIView animateWithDuration:animateTime animations:^{
        self.mainV.frame = [UIScreen mainScreen].bounds;
    }completion:^(BOOL finished) {
        [UIView animateWithDuration:animateTime animations:^{
            // 计算偏移量
            self.mainV.frame = [self frame:self.mainV.frame witOffsetX:offsetX];
        }];
    }];
//        self.mainV.frame = [UIScreen mainScreen].bounds;
    NSLog(@"%@",NSStringFromCGRect(self.mainV.frame));
}else{
    [UIView animateWithDuration:animateTime animations:^{
        // 计算偏移量
        self.mainV.frame = [self frame:self.mainV.frame witOffsetX:offsetX];
    }];
}
```