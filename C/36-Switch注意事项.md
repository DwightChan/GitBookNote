[TOC]

----

# Switch注意事项

##本小节知识点:
1. 【掌握】case语句的穿透问题
2. 【掌握】switch条件类型
3. 【掌握】case值的规定
4. 【掌握】default的位置问题

---

##1.【掌握】case的穿透问题

- switch里面的case只要匹配一次其它的都失效，包括default. 正是因为switch的这个特性, 所以可能导致程序出现逻辑错误

- 为了避免上述情况,C语言还􏰀供了一种break语句,专用于跳出switch语句,break语句只有关键字break,没有参数。在后面还将详细介绍。修改
    + 在每一case语句之后增加 break 语句,使每一次执行之后均可跳出switch语句,从而避免输出不应有的结果
    + 有时候也可用巧妙的利用case的穿透问题来简化代码

- 示例
```c
    int num;
    printf("输入一个1-7之间的数: ");
    scanf("%d",&num);
    switch (num){
        case 1:
            printf("玉米炒葡萄\n");
        //    break;
        case 2:
            printf("月饼炒辣椒\n");
        //    break;
        case 3:
            printf("爆炒妙脆角\n");
        //    break;
        case 4:
            printf("番茄炒卤蛋\n");
        //    break;
        case 5:
            printf("南瓜炒猪肝\n");
        //    break;
        case 6:
            printf("苹果炒西瓜\n");
        //    break;
        case 7:
            printf("天地无极\n");
        //    break;
        default:
            printf("error\n");
        //    break;
    }
输入1之后的输出结果:
玉米炒葡萄
月饼炒辣椒
爆炒妙脆角
番茄炒卤蛋
南瓜炒猪肝
苹果炒西瓜
天地无极
error
```

---

##2.【掌握】switch条件类型

- 表达式的类型(case语句后的值)必须是整型或可以转变为整型的值 (short、char和int类型)。

```c
 switch (10.10){ // 报错
        case 1:
            printf("玉米炒葡萄\n");
            break;
        default:
            printf("error\n");
            break;
    }
```
---

##3.【掌握】case值的规定

- case的值必须是是整型或可以转变为整型的值
```c
 switch (10){
        case 1:
            printf("玉米炒葡萄\n");
            break;
        case 'a': // 字符可以转换为整型
            printf("玉米炒葡萄\n");
            break;
        case 10.8: // 报错
            printf("玉米炒葡萄\n");
            break;
        default:
            printf("error\n");
            break;
    }
```

- case的值1、值2...值n只能为常数或常量,不能为变量。
```
 int num = 5;
 switch (10){
        case num: // 变量报错
            printf("玉米炒葡萄\n");
            break;
        default:
            printf("error\n");
            break;
    }
```

- 如果在case后面定义的变量必须加上大括号
```

 switch (10){
        case num:{
            int num = 5;
            printf("num = %d", num);
            break;
        }
        default:
            printf("error\n");
            break;
    }
```
- switch中case后面的表达式的值不能相同
```
 switch (10){
        case 1:
            printf("玉米炒葡萄\n");
            break;
        case 1: // 和上面相同报错
            printf("玉米炒葡萄\n");
            break;
        default:
            printf("error\n");
            break;
    }
```
- case语句可以有任意多句,可以不用加括号“{}”
```
 switch (10){
        case 1:
            printf("玉米炒葡萄1\n");
            printf("玉米炒葡萄2\n");
            break;
        default:
            printf("error\n");
            break;
    }
```

---

##4.【掌握】default的位置问题

- default可以省略
```c
 switch (10){
        case 1:
            printf("玉米炒葡萄1\n");
            break;
    }
```

- default语句可以写在switch语句中的任意位置
```c
 switch (10){
        default:
            printf("error\n");
            break;
        case 1:
            printf("玉米炒葡萄1\n");
            break;
    }
```
+ 执行流程:在执行的过程中,如果遇到break语句,则跳出switch语句。如果没有遇到break语句,则一直执行到switch语句的结束。

---




