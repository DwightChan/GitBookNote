

[TOC]

---

# sizeof运算符

---

##1.【了解】sizeof运算符介绍

- sizeof可以用来计算一个变量或一个常量、一种数据类型所占的内存字节数
    + 格式: 用法:sizeof(常量/变量)
    + **注意: sizeof不是一个函数, 是一个运算符. (面试题)**

---

##2.【理解】基本形式基本形式(用法)

- sizeof( 变量\常量 )
    + `sizeof(10); `
    + ```char c = 'a'; sizeof(c);```

- sizeof 变量\常量
    + ```sizeof 10; ```
    + ```char c = 'a'; sizeof c;```

- sizeof( 数据类型 )
    + ```sizeof(float);```
    + **注意:如果是数据类型不能省略括号**
        + `sizeof float; // 错误写法`

---


