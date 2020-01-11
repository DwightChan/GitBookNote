# 补充02:自定义跳转

```objc
1.当我们实际开发中有可能会做当跳转控制器的时候,通过自定义动画来实现跳转,过程如下
*1.首先我们需要确定一个对象,谁来负责进行跳转,我们通过UIPresentationController这个对象来负责进行转场,
   这个对象可以关联两个对象,一个是负责展示新的控制器的控制器,一个是展示出来的控制器,
*2.清楚这点后,我们需要来确定一个这样的控制器,在这里我们通过一个代理方法来确定这个控制器,
   就像tableView一样,我们通过tableView的数据源方法来确定展示怎么样的cell,
   那么这里我们只需要通过遵循UIViewControllerTransitioningDelegate协议,来通过这个协议里的这个方法:
- (nullable UIPresentationController *)presentationControllerForPresentedViewController:(UIViewController *)presented presentingViewController:(UIViewController *)presenting sourceViewController:(UIViewController *)source
来确定谁来负责展示,也即是确定我们需要的UIPresentationController.
*3.确定后,我们就可以通过这个控制器中的一些方法来负责展示,修改我们展示的视图的大小,但是我们必须设置
   我们展示的样式为自定义(twoVc.modalPresentationStyle = UIModalPresentationCustom)
*4.修改后,我们可以通过UIPresentationController的
- (CGRect)frameOfPresentedViewInContainerView来确定展示的视图的大小
*5.这里面需要了解两个类,第一个类名称:containerView:这个是用来表示展示控制器的视图,
   presentedView用来表示展示出来的的控制器的视图
*6.确定好这个后,我们只是修改了展示出视图的位置大小,但是动画没有改变,我们就需要改变动画,
   那么首先我们必须确定谁来负责当弹出控制器时的动画,以及销毁控制器时的动画,
*7.我们可以通过UIViewControllerTransitioningDelegate中的方法(下面的方法)
//用来表示当展示一个控制器的时候,谁来负责动画
- (nullable id <UIViewControllerAnimatedTransitioning>)animationControllerForPresentedController:(UIViewController *)presented presentingController:(UIViewController *)presenting sourceController:(UIViewController *)source{
    return self;
    
    
}
//用来表示当一个控制器销毁的时候,谁来负责动画
- (nullable id <UIViewControllerAnimatedTransitioning>)animationControllerForDismissedController:(UIViewController *)dismissed{
    return self;
    
}

通过这连个代理方法就可以确定谁来负弹出控制器时的动画,以及销毁控制器时的动画

*8.在这两个方法中,需要的对象只要遵循协议即可,所以我们可以让当前的控制器遵循协议,
   然后,设置self即可
*9.设置好谁来展示动画后,我们需要来通过UIViewControllerAnimatedTransitioning
   这个协议中的方法来确定怎样展示动画.以及动画的时间
*10.我们通过下面的方法来确定动画的时间,以及怎样展示动画
//动画的时间
- (NSTimeInterval)transitionDuration:(nullable id <UIViewControllerContextTransitioning>)transitionContext{
    
    return 2.0;
}
// This method can only  be a nop if the transition is interactive and not a percentDriven interactive transition.
//怎样展示动画
- (void)animateTransition:(id <UIViewControllerContextTransitioning>)transitionContext{
    //    1.获取将要展示的视图
    UIView *toView =   [transitionContext viewForKey:UITransitionContextToViewKey];
    //    2.设置动画
    CGRect tempFrame = toView.frame;
    tempFrame.origin.y = - toView.frame.size.height;
    toView.frame = tempFrame;
    [UIView animateWithDuration:2.0 animations:^{
        CGRect tempFrame = toView.frame;
        tempFrame.origin.y = 0;
        toView.frame = tempFrame;
    } completion:^(BOOL finished) {
        //        凡是自定义动画,在动画结束的时候,必须告诉系统动画结束
        [transitionContext completeTransition:YES];
    }];
    
    
    
}

*11.transitionContext这个对象是我们最重要的对象,可以获取很多值,
这里面刚才所有得方法都是固定的,除了
- (void)animateTransition:(id <UIViewControllerContextTransitioning>)transitionContext
这个设置动画的方法,我们以后只需要设置这个方法即可
*12.这里面我们还需要注意两个对象:toView:表示我们要到达的视图,这里和我们的presentedView是一样的,
   还有fromeView:表示我们从哪个视图进行动画,这里现在和congtainerView是一样的
   
综合上述,这里我们今天制作了解,后续我还会讲解一次.大家先有个认识即可
```
