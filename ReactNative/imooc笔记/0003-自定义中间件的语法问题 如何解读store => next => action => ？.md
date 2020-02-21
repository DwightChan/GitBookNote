[toc]

---

# 自定义中间件的语法问题 如何解读store => next => action => ？



## 问题: 老师 我不太明白这段代码的意思，能麻烦您再给我解释一下吗

```
const logger = store => next => action => {//这句

    if (typeof action === 'function'){
        console.log('dispatching a function');
    }else{
        console.log('dispatching',action);
    }

    const result = next(action);//还有这一句
    console.log('nextState', store.getState());
    return result;

};
```

## 解答:

store => next => action =>是JS柯里化 + 箭头函数语法的应用：

```
/**
 * 自定义log中间件
 * @param store
 * @returns {function(*): Function}
 */
const logger = store => next => action => {
    if (typeof action === 'function') {
        console.log('dispatching a function');
    } else {
        console.log('dispatching', action);
    }
    const result = next(action);
    console.log('nextState', store.getState());
    return result;
};
```

等价于：

```
const logger = (store) => {
    return (next) => {
        return (action) => {
            if (typeof action === 'function') {
                console.log('dispatching a function');
            } else {
                console.log('dispatching', action);
            }
            const result = next(action);
            console.log('nextState', store.getState());
            return result;
        };
    };
};
```



## 关于柯里化可参考：
- [图解Redux中middleware的洋葱模型](https://github.com/fi3ework/blog/issues/14)
- [JavaScript 柯里化](https://juejin.im/post/5af13664f265da0ba266efcf)
