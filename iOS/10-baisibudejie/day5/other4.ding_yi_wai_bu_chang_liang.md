# 定义外部常量

- **注意: 这里不需要类名**
    - 即是不需要像某个类那样要 `@interface 类名   ... @end 这样写`
- 同样其他类需要使用的时候, 只要包含头文件名的`.h`头即可, 如: `#import "CDHConst.h"`即可



- **`.h`文件**

  ```objc
  //
  //  CDHConst.h
  //  BuDeJie
  //
  //  Created by chendehao on 15/4/14.
  //  Copyright © 2015年 陈德豪. All rights reserved.
  //

  #import <UIKit/UIKit.h>

  /** 导航栏的最大 Y 值(底部) */
  UIKIT_EXTERN CGFloat const CDHNavBarMaxy;

  /** TabBar 的高度 */
  UIKIT_EXTERN CGFloat const CDHTabBarH;

  /** 标题栏的高度 */
  UIKIT_EXTERN CGFloat const CDHTitleViewH;

  /** 请求路径 */
  UIKIT_EXTERN NSString * const CDHRequestURL;
  ```



- **`.m`文件**

  ```objc
  //
  //  CDHConst.m
  //  BuDeJie
  //
  //  Created by chendehao on 15/4/14.
  //  Copyright © 2015年 陈德豪. All rights reserved.
  //

  //#import <UIKit/UIKit.h>// 用这个也可以, 用下面这行也行
  #import "CDHConst.h"

  /** 导航栏的最大 Y 值(底部) */
  CGFloat const CDHNavBarMaxy = 64;

  /** TabBar 的高度 */
  CGFloat const CDHTabBarH = 49;

  /** 标题栏的高度 */
  CGFloat const CDHTitleViewH = 35;
  /**  请求路径 */
  NSString * const CDHRequestURL = @"http://api.budejie.com/api/api_open.php";
  ```