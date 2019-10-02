[TOC]

---

# do-while和while对比

---

##1.【掌握】do-while和while对比

- while, 先判断再执行
```c
    int x = 0;
    while (x < 0) {
        x++;
    }
     printf("x = %d\n", x);
输出结果:x =  0
```
- do-while, 先执行再执行
```c
    int y = 0;
    do {
        y++;
    } while (y < 0);
    printf("y = %d\n", y);
输出结果:x =  1
```


