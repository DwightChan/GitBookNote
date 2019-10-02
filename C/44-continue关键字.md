[TOC]

---

# continue关键字



---

##1.【掌握】continue关键字

- continue语句的作用是跳过循环体中剩余的语句而继续下一次

- 使用场合:
    + 循环结构

![](images/continue.png)

- 练习: 把100~200之间的不能被3整除的数输出
```c
for(int i = 100; i<= 200; i++)
{
    if(i %3 == 0) continue;
    printf("i = %d", i);
}
```


