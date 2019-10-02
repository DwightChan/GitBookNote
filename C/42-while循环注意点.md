[TOC]



---

# while循环注意点

---

##1.【掌握】while循环的陷阱

- 任何数值都有真假性
```c
    while (1) {//死循环
        printf("123\n");
    }
    printf("123\n"); // 永远执行不到
```
- 当一个变量与一个常量进行== 或 != 的时候,通常把常量写在前面
```c
    int num = 3;
    while (3 == num) {
        printf("num = %d\n",num);
        num++;
    }
```
- while 后如果只有一条语句它可以省略大括号
    + 空语句它也是一条语句
    + while小阔号后面不可以直接写分号
```c
    // while省略大阔号的时候条件满足就会执行while后面的第一条语句
    while (0)
       printf("123\n");
    printf("456\n");
```
- 作用域问题
```c
    while (1) {
        int a = 10;
    }
    printf("a = %d\n", a); // 访问不到

    while (0)
        int a = 10; // 作用域混乱
     printf("a = %d\n", a);
```
- 分号问题
```c
    while (1);//空语句
    {
        printf("123\n");
    }
```
- 最简单的死循环
```c
    while (1);
```
---


