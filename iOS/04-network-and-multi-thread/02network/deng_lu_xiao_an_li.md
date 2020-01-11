# 登录小案例
<br/>
####1. 相关知识点
- 发送POST请求的过程
- SVProgressHUD框架的使用
- 字符串截取处理

---
<br/>
####2. 业务逻辑

- **设置弹窗的样式**
    - 设置为正在登入时, 不可以再输入用户名和密码等信息
    - 设置弹窗的的颜色


- **得到用户的输入**


- **校验用户输入**
    - 用户名是否有输入,如果没有则 HUD 有相应的提示
    - 密码是否有输入,如果没有则 HUD 有相应的提示


- **确定请求路径**

- **用 post 请求, 用户名和密码是比较隐私**
    - 创建可变请求对象
    - 修改请求方法
    - 设置参数
        - 中文转码


- **创建会话对象**


- **创建 task**
    - task 回调解析响应数据
    - 字符截串, 获得特定的数据 (这里可以不用这种方法)
        - **注意**: 在截取的时候不要将长度写死, 避免获取到不同结果时, 需要截取的长度不同的情况;
        - **注意**: 如果是返回的响应体的数据比较大的话, 那就不好截取了, 所以这种办法只用于小数据, 这里用下面方法
    - 直接通过判断返回的数据包含的是 error 还是 success
    - 弹窗提示用户登入是否成功
        - **注意:** 线程通信, 先回到主线程在做弹窗提示
        - 处理弹窗中显示的内容
            - 含有的是 error , 则调用的是showErrorWithStatus: 方法
            - 含有的是 success, 则调用的是showSuccessWithStatus:方法
    - 取消弹窗 HUD
        - **注意: **线程通信, 先回到主线程在做取消弹窗


- **执行 task 任务**


- **弹窗 HUD , 在 task 任务之后**
    - 弹窗添加显示文字 "正在登入..."

---
<br/>
####3. 实例代码
```objc
//
//  ViewController.m
//  01-掌握-登录小案例
//
//  Created by chendehao on 16/6/20.
//  Copyright © 2016年 chendehao. All rights reserved.
//

#import "ViewController.h"
#import "SVProgressHUD.h"

@interface ViewController ()
@property (weak, nonatomic) IBOutlet UITextField *usernameTF;
@property (weak, nonatomic) IBOutlet UITextField *passwordTF;
@end

//模拟器切换到电脑键盘输入  shift  + command + k

@implementation ViewController
- (IBAction)loginBtnClick:(id)sender{
    //设置背景色和灰色HUD
    [SVProgressHUD setDefaultMaskType:SVProgressHUDMaskTypeBlack];
    [SVProgressHUD setDefaultStyle:SVProgressHUDStyleDark];
    
    //1. 得到用户的输入
    NSString *usernameStr = self.usernameTF.text;
    NSString *passwordStr = self.passwordTF.text;
    
    //2. 校验用户的输入
    if (usernameStr.length == 0) {
        [SVProgressHUD showErrorWithStatus:self.usernameTF.placeholder];
        return;
    }
    
    if (passwordStr.length == 0) {
        [SVProgressHUD showErrorWithStatus:self.passwordTF.placeholder];
        return;
    }
    
    //确定请求路径
    NSURL *url = [NSURL URLWithString:@"http://120.25.226.186:32812/login"];
    
    //创建可变请求对象
    NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
    
    //修改请求方法
    request.HTTPMethod = @"POST";
    
    //设置参数 这里的 type 的参数可传可不传, 如果不传默认就 JSON
    NSString *bodyStr = [NSString stringWithFormat:@"username=%@&pwd=%@&type=JSON",usernameStr,passwordStr];
    request.HTTPBody = [bodyStr dataUsingEncoding:NSUTF8StringEncoding];
    
    //创建会话对象
    NSURLSession *session = [NSURLSession sharedSession];
    
    //创建Task
    NSURLSessionDataTask *dataTsk =[session dataTaskWithRequest:request completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {
        
        //解析数据
        NSString *resultStr = [[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding];
        NSLog(@"%@",resultStr);
        
        NSDictionary *dict = [NSJSONSerialization JSONObjectWithData:data options:kNilOptions error:nil];
        
        NSString *msg = nil;
        if ([resultStr containsString:@"error"]) {
            msg = dict[@"error"];
            [SVProgressHUD showErrorWithStatus:msg];
        }else
        {
            msg = dict[@"success"];
            [SVProgressHUD showSuccessWithStatus:msg];
        }
        /*
         这里的'\' 是作为转译
        NSUInteger loc = [resultStr rangeOfString:@":\""].location + 2;
        NSUInteger len = [resultStr rangeOfString:@"\"}"].location - loc;
        
        NSString *msg = [resultStr substringWithRange:NSMakeRange(loc, len)];
        
//        // 注意: 一定要回到主线程取消蒙板
//        dispatch_async(dispatch_get_main_queue(), ^{
//            [SVProgressHUD dismiss];
//        });
         
        dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(2.0 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
            if ([resultStr containsString:@"error"]) {
                [SVProgressHUD showErrorWithStatus:msg];
            }else{
                [SVProgressHUD showSuccessWithStatus:msg];
            }
        });
         */
    }];
    
    //执行TASK
    [dataTsk resume];
    
    //弹出HUD
    [SVProgressHUD showWithStatus:@"正在登陆..."];
}
// 所谓请求失败是没有拿到服务器发送过来的数据,
// 服务器想给请求者什么数据, 是服务器设置
@end
```

---
<br/>