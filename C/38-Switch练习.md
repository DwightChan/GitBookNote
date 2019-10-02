[TOC]

---

# Switch练习



---

##1.【了解】判断季节

- 从键盘输入一个月份,输出对应季节 12~2 冬季 3~5 春季 6~
8 夏季 9~11 秋季(用switch)

```c
思路:
1.提􏰀示用户输入一个月份
2.接收一个月份
3.判断
case 12:
case 1:
case 2:
冬季
break;
```
> + 巧用省略break
---

##2.【了解】实现计算器

- 使用Switch实现简单的计算器
```c
 思路:
 让用户输入一个数
 让用户再输入一个符号
 让用户输入另外一个数
 计算结果

    int num1,num2,op,result; printf("请输入第一个数字\n");
    scanf("%d",&num1);
    printf("请输入运算符: 1 加法 2 减法 3 乘法 4 除法\n");
    scanf("%d",&op);
    printf("请输入第二个数字:\n"); scanf("%d",&num2);
    switch (op) {
        case 1:
            result = num1+num2;
            break;
        case 2:
            result = num1-num2;
            break;
        case 3:
            result = num1*num2;
            break;
        case 4:
            result = num1/num2;
            break;
        default:
            printf("error!"); break;
    }
    printf("计算结果:%d\n",result);
```
---

