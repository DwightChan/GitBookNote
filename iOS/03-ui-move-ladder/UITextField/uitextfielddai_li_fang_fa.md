# UITextField代理方法
- **可以通过设置代理的方式来去监听文件框的改变**
- **可以通过代理方法拦截用户输入, 自定义输入弹窗等**

- 是否允许开始编辑

  ```objc
  - (BOOL)textFieldShouldBeginEditing:(UITextField *)textField{
      return YES;
  }
  ```

- 开始编辑时调用,(弹出键盘)became first responder

  ```objc
  - (void)textFieldDidBeginEditing:(UITextField *)textField{
      NSLog(@"弹出键盘");
  }
  ```

- 是否允许结束编辑.

  ```objc
  - (BOOL)textFieldShouldEndEditing:(UITextField *)textField{
      return YES;
  }
  ```


- 结束编辑时调用.

  ```objc
  - (void)textFieldDidEndEditing:(UITextField *)textField{
      NSLog(@"结束编辑时调用.");
  }
  ```

- 是否允许文字改变.
    - 拦截用户输入.
    - **注意**: 这里得到的 参数 string 如果要显示在 UITextField 上必须等该方法返回 YES 之后才有效.

  ```objc
  - (BOOL)textField:(UITextField *)textField shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string{
      return NO;
  }
  ```


---
<br/>
