# Xcode设置
##本小节知识点:
1. 【掌握】如何关闭ARC功能
2. 【掌握】如何开启僵尸对象监控

---

##1.如何关闭ARC功能
- 要想手动调用retain、release等方法 , 就必须关闭ARC功能

![](images/06xcodeshe_zhi/Snip20150619_3.png)

##2.如何开启僵尸对象监控
- 默认情况下，Xcode是不会管僵尸对象的，使用一块被释放的内存也不会报错。为了方便调试，应该开启僵尸对象监控


![](images/06xcodeshe_zhi/Snip20150619_4.png)

![](images/06xcodeshe_zhi/Snip20150619_5.png)


---


