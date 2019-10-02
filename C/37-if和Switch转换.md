[TOC]

---

# if和Switch转换

---

##1.【了解】if语句和switch语句转换

- 利用if实现
```c
    要求用户输入一个分数，根据输入的分数输出对应的等级
     A 90～100  99/10 = 9  90/10= 9  98/10 = 9 100/10 = 10
     B 80～89 89/10 = 8
     C 70～79
     D 60～69
     E 0～59
```
```c
//    1.提示用户输入学生的分数
    printf("请输入一个0～100的分数\n");
//    2.定义变量保存用户输入的分数
    int score = -1;
//    3.接收用户输入的分数
    scanf("%d", &score);
//    4.判断用户输入的分数输出对应的等级
    if (score >= 90 && score <= 100) {
        printf("A\n");
    }else if (score >= 80 && score <= 89)
    {
        printf("B\n");
    }else if (score >= 70 && score <= 79)
    {
        printf("C\n");
    }else if (score >= 60 && score <= 69)
    {
        printf("D\n");
    }else if (score >= 0 && score <= 59)
    {
        printf("E\n");
    }else{
        printf("少喝点三鹿\n");
    }
```

- 利用switch实现
```c
 switch (score/10) {
        case 10:
        case 9:
            printf("A\n");
            break;
        case 8:
            printf("B\n");
            break;
        case 7:
            printf("D\n");
            break;
        case 6:
            printf("C\n");
            break;
          default:
            printf("E\n");
            break;
    }
```

##2.【了解】if语句和switch语句选择

- 分支比较多且无法穷尽或进行大量列举 时最好用if, Switch对遇见判断非常不利
- 如果数据量不是很大, 并且数据是固定的可以用Switch
- 理论上Switch的效率比if高

- 判断用户输入的数是否大于100:
    + if实现
```c
    int a = -1;
    scanf("%d", &a);
    if (a > 100) {
        printf("大于\n");
    }
```
+ switch实现

```c
    // 挺(T)萌(M)的(D)搞不定啊
    int b = 5;
    switch (a) {
        case 1:
        case 2:
        case 3:
        case 4:
        case 5:
            printf("大于\n");
            break;
        default:
            break;
    }
```
---


