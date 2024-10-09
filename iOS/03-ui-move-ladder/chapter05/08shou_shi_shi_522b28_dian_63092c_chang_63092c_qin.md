# 08-手势识别(点按,长按,轻扫)

```objc
//
//  ViewController.m
//  My-手势识别
//
//  Created by Dwight on 16/6/4.
//  Copyright © 2016年 chendehao. All rights reserved.
//

#import "ViewController.h"

@interface ViewController ()<UIGestureRecognizerDelegate>
@property (weak, nonatomic) IBOutlet UIImageView *imageView;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
//     允许交互事件
    self.imageView.userInteractionEnabled = YES;
    
    
//     点按手势
    [self tapGes:self];  
//     长按手势
    [self longPressGes:self]; 
//     轻扫手势
//    [self swipeGes:self];
//     拖动手势
    [self panGes:self];
//     旋转手势
    [self rotationGes:self];
//    捏合手势
    [self pinckGes:self]; 
}

#pragma mark - 手势
//======================================手势==========================================
// 点按手势
- (void)tapGes:(id<UIGestureRecognizerDelegate>)delegate{
    // 创建一个点按手势
    UITapGestureRecognizer *tap = [[UITapGestureRecognizer alloc]initWithTarget:self action:@selector(tap)];
    // 设置代理
    tap.delegate = delegate;
    // 添加点按手势
    [self.imageView addGestureRecognizer:tap];
}
// 当点按时调用
- (void)tap{
    NSLog(@"%s",__func__);
}

// 长按手势
- (void)longPressGes:(id<UIGestureRecognizerDelegate>)delegate{
    // 创建一个长按手势
    UILongPressGestureRecognizer *longPress = [[UILongPressGestureRecognizer alloc]initWithTarget:self action:@selector(longPress:)];
    // 设置代理
    longPress.delegate = delegate;
    // 给图片添加这个手势
    [self.imageView addGestureRecognizer:longPress];
    
}
// 长按时调用
- (void)longPress:(UILongPressGestureRecognizer *)longP{
    if (longP.state == UIGestureRecognizerStateBegan) {
        NSLog(@"began");
    }else if(longP.state == UIGestureRecognizerStateChanged){
        NSLog(@"UIGestureRecognizerStateChanged");
    }else if(longP.state == UIGestureRecognizerStateEnded){
        NSLog(@"UIGestureRecognizerStateEnded");
    }
}

// 轻扫手势
- (void)swipeGes:(id<UIGestureRecognizerDelegate>)delegate{
    // 注意01: 轻扫手势要有方向,如果不设置轻扫手势,默认只有左往右扫有效
    // 注意02: 轻扫手指可以通过 | 或运算符添加多个方向,
    //        同时要注意或运算符只能同时或左|右 / 上|下, 不能或 上|左,下|左 即是只能 横|横,纵|纵 ,不能 横|纵
    //        如果使用或运算符之后 横|纵 , 纵|横 ,不论先后编译之后都只保留有横向的手势
    // 注意03: 如果要判断手势的方向,就不能通过或运算符添加手势,只能每一个方向设置一个手势
    
    // 创建轻扫手势 向左的手势
    UISwipeGestureRecognizer *swipeToLeft = [[UISwipeGestureRecognizer alloc]initWithTarget:self action:@selector(swipe:)];
    // 手势设置轻扫的方向
    swipeToLeft.direction = UISwipeGestureRecognizerDirectionLeft ;
    // 设置代理
    swipeToLeft.delegate = delegate;
    // 添加手势
    [self.imageView addGestureRecognizer:swipeToLeft];
    
    // 向右的手势
    UISwipeGestureRecognizer *swipeToRight = [[UISwipeGestureRecognizer alloc]initWithTarget:self action:@selector(swipe:)];
    swipeToRight.direction = UISwipeGestureRecognizerDirectionRight;
    swipeToRight.delegate = delegate ;
    [self.imageView addGestureRecognizer:swipeToRight];
    
    // 向上的手势
    UISwipeGestureRecognizer *swipeToUp = [[UISwipeGestureRecognizer alloc]initWithTarget:self action:@selector(swipe:)];
    swipeToUp.direction = UISwipeGestureRecognizerDirectionUp;
    swipeToUp.delegate = delegate ;
    [self.imageView addGestureRecognizer:swipeToUp];
    
    // 向下的手势
    UISwipeGestureRecognizer *swipeToDown = [[UISwipeGestureRecognizer alloc]initWithTarget:self action:@selector(swipe:)];
    swipeToDown.direction = UISwipeGestureRecognizerDirectionDown;
    swipeToDown.delegate = delegate;
    [self.imageView addGestureRecognizer:swipeToDown];
    
}
// 轻扫手势是调用
- (void)swipe:(UISwipeGestureRecognizer *)swipe{
    if (swipe.direction == UISwipeGestureRecognizerDirectionLeft) {
        NSLog(@"向左划了一下");
    }else if(swipe.direction == UISwipeGestureRecognizerDirectionRight){
        NSLog(@"向右划了一下");
    }else if(swipe.direction ==  UISwipeGestureRecognizerDirectionUp){
        NSLog(@"向上划了一下");
    }else if(swipe.direction == UISwipeGestureRecognizerDirectionDown){
        NSLog(@"向下划了一下");
    }
}

// 拖拽手势
- (void)panGes:(id<UIGestureRecognizerDelegate>)delegate{
    // 创建一个拖拽手势
    UIPanGestureRecognizer *pan = [[UIPanGestureRecognizer alloc]initWithTarget:self action:@selector(pan:)];
    // 设置代理
    pan.delegate = delegate;
    // 给图片添加拖拽手势
    [self.imageView addGestureRecognizer:pan];
}
// 拖拽是调用这个方法
- (void)pan:(UIPanGestureRecognizer *)pan{
    //    NSLog(@"%s",__func__);
    //    获取偏移量
    //    相对于原始的偏移量
    CGPoint transP = [pan translationInView:self.imageView];
    NSLog(@"%@",NSStringFromCGPoint(transP));
    //    平移(方法一:)
    //    注意: 平移的时候如果使用的是带 make 的方法在每一次平移都是相对一原始位置,
    //          如果图片已经被平移过,不在原始位置,当再次做平移,图片先自动回到原始位置,在做平移
    //          (这就有可能导致图片不在手指下面了),但只要不松手继续移动,这时候图片就又从原始位置开始移动
    //    self.imageView.transform = CGAffineTransformMakeTranslation(transP.x, transP.y);
    
    //    平移(方法二:)
    //    注意: 这里使用的是没有带 make 平移方法,这个方法是相对于上一次的位置来说的,
    //          但我们获取到的偏移量是相对于最原始的,如此一来每次平移的偏移量都会有积累,每走一步的跨度会也来越大
    //          很快就难以控制被移除屏幕范围,所以我们必须每次移动之后就就要将当前点的值赋给原始位置对应的变量
    //          这样下次改变了原始位置点的坐标之后,下次再来平移也就是相对于上次的位置了
    self.imageView.transform = CGAffineTransformTranslate(self.imageView.transform, transP.x, transP.y);
    //    复位(清零),设置当前点为下一次的原始位置点,即是下次的原始位置就是这一次平移之后的点,
    //    这就与不带 make 的方法对应上了,每一都是相对于上次的位置来做平移;
    [pan setTranslation:CGPointMake(0, 0) inView:self.imageView];
    //    [pan setTranslation:CGPointZero inView:self.imageView];// 等效于上面  
}


// 旋转手势
- (void)rotationGes:(id<UIGestureRecognizerDelegate>)delegate{
    // 创建一个旋转手势
    UIRotationGestureRecognizer *rotationGes = [[UIRotationGestureRecognizer alloc]initWithTarget:self action:@selector(rotation:)];
    // 设置代理
    rotationGes.delegate = delegate;
    // 添加旋转手势
    [self.imageView addGestureRecognizer:rotationGes];   
}
// 旋转时调用这个方法
- (void)rotation:(UIRotationGestureRecognizer *)rotationGes{
    
    //    旋转(方法一:)
    //    注意: 旋转的时候如果使用的是带 make 的方法在每一次旋转都是相对一原始角度,
    //          如果图片已经被旋转过,不在原始角度,当再次做旋转是,图片先自动回到原始角度,再做旋转
    //    self.imageView.transform = CGAffineTransformMakeRotation(rotationGes.rotation);
    
    //    旋转(方法二:)
    //    注意: 旋转的时候如果使用的是不带 make 的方法在每一次旋转都是相对一上一次角度,
    //          但是通过获取到的 rotation (角度)是相对与原始角度来说的,这样直接用于将数据不带 make 的方法中
    //          然而每次不带 make 的方法又是相对与上次角度来说,就有了累积角度的效果,每转一弧度都有会积累,
    //          转的弧度只会越来越大,很快就变成风扇在转了
    self.imageView.transform = CGAffineTransformRotate(self.imageView.transform, rotationGes.rotation);
    //    复位(清零),设置当前角度为下一次的原始角度,即是下次的原始角度就是这一次旋转之后的角度,
    //    这就与不带 make 的方法对应上了,每一都是相对于上次的角度来做旋转;
    rotationGes.rotation = 0;
}

// 捏合手势
- (void)pinckGes:(id<UIGestureRecognizerDelegate>)delegate{
    // 创建捏合手势
    UIPinchGestureRecognizer *pinch = [[UIPinchGestureRecognizer alloc]initWithTarget:self action:@selector(pinch:)];
    // 设置代理
    pinch.delegate = delegate;
    // 给图片添加手势
    [self.imageView addGestureRecognizer:pinch];
}
// 捏合时调用这个方法
- (void)pinch:(UIPinchGestureRecognizer *)pinchGes{
    // 捏合手势
    //    捏合(方法一:)
    //    注意: 捏合的时候如果使用的是带 make 的方法在每一次捏合都是相对一原始尺寸,
    //          如果图片已经被捏合(放大或缩小)过,不是原来的尺寸,当再次做捏合时,图片先自动回到原始尺寸,再开始捏合
    //    self.imageView.transform = CGAffineTransformMakeScale(pinchGes.scale, pinchGes.scale);
    
    //    捏合(方法二:)
    //    注意: 捏合的时候如果使用的是不带 make 的方法在每一次捏合都是相对一上一次尺寸大小,
    //          但是通过获取到的 scale (缩放比例)是相对与原始尺寸来说的,这样直接将数据用于不带 make 的方法中
    //          然而每次不带 make 的方法又是相对与上次角度来说,就有了累积比例的效果,每捏合一次都是与上一次的比率的乘积,
    //          比例只会越来越大或者越来越小,很快就看不到图片了
    self.imageView.transform = CGAffineTransformScale(self.imageView.transform, pinchGes.scale, pinchGes.scale);
    //    比率复1,设置当前大小为下一次的原始大小,即是下次的原始大小就是这一次捏合之后的的大小;
    //    这就与不带 make 的方法对应上了,每一都是相对于上次的大小来做捏合;
    pinchGes.scale = 1;
}


#pragma mark - delegate
// ===================================================================================
// 是否允许接收新闻  注意这里的 press 不是按/压的意思,而是新闻消息
//- (BOOL)gestureRecognizer:(UIGestureRecognizer *)gestureRecognizer shouldReceivePress:(UIPress *)press{
//    return  NO;
//}

// 是否允许接收手指
//- (BOOL)gestureRecognizer:(UIGestureRecognizer *)gestureRecognizer shouldReceiveTouch:(UITouch *)touch{
//    // 获取当前点
//    CGPoint curP = [touch locationInView:self.imageView];
//    // 左边能点,右边不能点
//    if (curP.x > self.imageView.bounds.size.width * 0.5) {
//        return NO;
//    }else{
//        return YES;
//    }
//}

// 是否允许同时支持多个手势
- (BOOL)gestureRecognizer:(UIGestureRecognizer *)gestureRecognizer shouldRecognizeSimultaneouslyWithGestureRecognizer:(UIGestureRecognizer *)otherGestureRecognizer{
    return YES;
}


@end
```