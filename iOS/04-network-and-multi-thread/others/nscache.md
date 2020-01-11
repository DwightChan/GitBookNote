# NSCache



##1. NSCache简单说明
- NSCache是苹果官方提供的缓存类，具体使用和NSMutableDictionary类似，在AFN和SDWebImage框架中被使用来管理缓存
- 苹果官方解释NSCache在系统内存很低时，会自动释放对象（但模拟器演示不会释放）
    - **建议**：接收到内存警告时主动调用removeAllObject方法释放对象
- NSCache是线程安全的，在多线程操作中，不需要对NSCache加锁
- NSCache的Key只是对对象进行Strong引用，不是拷贝，在清理的时候计算的是实际大小而不是引用的大小

---
<br/>

##2. NSCache属性和方法介绍
- **属性介绍**
    - name:名称
    - delegete:设置代理
    - totalCostLimit：缓存空间的最大总成本，超出上限会自动回收对象。默认值为0，表示没有限制
    - countLimit：能够缓存的对象的最大数量。默认值为0，表示没有限制
    - evictsObjectsWithDiscardedContent：标识缓存是否回收废弃的内容


- **方法介绍**
    - `- (void)setObject:(ObjectType)obj forKey:(KeyType)key;`
        - 在缓存中设置指定键名对应的值，0成本
    - `- (void)setObject:(ObjectType)obj forKey:(KeyType)keycost:(NSUInteger)g;`
        - 在缓存中设置指定键名对应的值，并且指定该键值对的成本，用于计算记录在缓存中的所有对象的总成本
        - 当出现内存警告或者超出缓存总成本上限的时候，缓存会开启一个回收过程，删除部分元素
    - `- (void)removeObjectForKey:(KeyType)key;`
        - 删除缓存中指定键名的对象
    - `- (void)removeAllObjects;`
        - 删除缓存中所有的对象


---
<br/>
