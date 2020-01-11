# 补充: 按钮的知识点

##1. 按钮的状态
- **1.UIControlStateNormal**
    - 除开UIControlStateHighlighted、UIControlStateDisabled、UIControlStateSelected以外的其他情况，都是normal状态
    - 这种状态下的按钮【可以】接收点击事件
    - 如果前后连着设置按钮同时处于多种状态, 则表现出来的也是 normal 状态, 除去如果有 设置为 enabled = NO; 则会进入UIControlStateDisabled状态(包括颜色), 不能点击

  ```objc
  //下面两种杂交在一起(就不是 normal 后面三种 ), 会显示为 Normal 状态的颜色, 但是 设置了 Enabled == NO,  所以这里也是不能点击的,
  self.button.selected = YES;
  self.button.enabled = NO;
  ```


- **2.UIControlStateHighlighted**
    - 【当按住按钮不松开】或者【highlighted = YES】时就能达到这种状态
    - 这种状态下的按钮【可以】接收点击事件
 

- **3.UIControlStateDisabled**
  - 【button.enabled = NO】时就能达到这种状态
  - 这种状态下的按钮【无法】接收点击事件


- **4.UIControlStateSelected**
    - 【button.selected = YES】时就能达到这种状态
    - 这种状态下的按钮【可以】接收点击事件

---


##2. 让按钮无法点击的2种方法
- **button.enabled = NO;**
     * 【会】进入UIControlStateDisabled状态


- **button.userInteractionEnabled = NO; **
     * 【不会】进入UIControlStateDisabled状态，继续保持当前状态


--- 
##3. 重写按钮的某个状态属性的 setter 方法和 getter 方法


- 如: 重写按钮高亮get方法, 如果返回值是 yes , 则永远返回的是高亮状态, 如果返回值是 NO 则永远返回的是非高亮

  ```objc
  - (BOOL)isHighlighted{
      return NO;
  }
  ```

- 重写按钮高亮 set 方法, 如果没有实现内部属性赋值(属性是父类定义的, 要调用父类的方法赋值), 则不会出现高亮状态
    - 如果给内部属性赋值为 Yes , 则会一直为 YES状态, 如果赋值为 NO,  则一直未 NO 状态

  ```objc
  - (void)setHighlighted:(BOOL)highlighted{
      [super setHighlighted:highlighted];
  }
  ```

---