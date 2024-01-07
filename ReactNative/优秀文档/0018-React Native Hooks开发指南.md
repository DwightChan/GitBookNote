## React Native Hooks开发指南

# React Native Hooks开发指南

![img](https://o.devio.org/images/rn2/rn-hooks.png)

## 什么是Hooks

Hooks 是 React 16.8 的新增特性。它可以让你在不编写 class 的情况下使用 state 以及其他的 React 特性。

Hooks 是一种在函数式组件中使用有状态函数的方法。

> Hooks不支持在class中使用，比如在class中使用useState和useEffect都是不允许的。

### Hooks的特性

在使用Hooks之前我们必须要要做明白一下几点：

- Hooks是完全可选的：

  在React Native项目中Hooks不是必须的，React推出Hooks不是为了替代class，而是对class的一种补充

  ；

  - 与其说Hooks是React新增的功能，倒不如说它是React新增的一种特性更为贴切；

- 不要为了Hooks而Hooks：Hooks只是React的一种新的写法，我们不必对已存在的项目通过Hooks重写，推荐小伙伴们可以对一些新的组件来尝试Hooks，这也是包括阿里在内的很多大厂通常的做法；

- Hooks100% 向后兼容的： Hooks 不包含任何新增的功能，完全兼容和class混用；

## 如何在React Native使用Hooks

Hooks最为常见的有两个API：`useState`与`useEffect`也叫`State Hook`与`Effect Hook`，那么接下来我们就来学习下在React Native中如何使用这两个API。

> 首先需要指出的是Hooks 是 React 16.8 的新增特性，因此我们不需要引入其它任何库，只需要确保项目依赖的React大于等于16.8即可。

### 在React Native中使用 State Hook

> 需求1：假如我们有个需求将从网络上请求到的数据显示在界面上，我们先看它的class写法：

```js
import React from 'react';
import {
    SafeAreaView,
    Text,
    TouchableOpacity
} from 'react-native';
import Constants from './expand/dao/Constants';
import { post } from './expand/dao/HiNet';

class HiNetDemo extends React.Component<{}, { msg: string }> {
    constructor(props: any) {
        super(props);
        this.state = {
            msg: ''
        }
    }
    doFetch = () => {
        const formData = new FormData();
        formData.append("requestPrams", 'RN');
        post(Constants.test.api)(formData)().then(result => {
            this.setState({
                msg: JSON.stringify(result)
            });
        }).catch(e => {
            console.log(e);
            this.setState({
                msg: JSON.stringify(e)
            });
        })
    }
    render() {
        return (
            <SafeAreaView>
                <TouchableOpacity onPress={this.doFetch}>
                    <Text>加载</Text>
                </TouchableOpacity>
                <Text>{this.state.msg}</Text>
            </SafeAreaView>
        );
    }
}
```

那么它对应的hooks写法该是怎样子的呢？

下面代码接借助RReact Native的[HiNet网络框架](https://coding.imooc.com/class/304.html)发出网络请求并通过`useState`来控制`msg`的状态，并将其展示在界面上：

```js
import React, { useState } from 'react';
import {
    SafeAreaView,
    Text,
    TouchableOpacity
} from 'react-native';
import Constants from './expand/dao/Constants';
import { post } from './expand/dao/HiNet';
export default (props: any) => {
    const [msg, setMsg] = useState('');
    const doFetch = () => {
        const formData = new FormData();
        formData.append("requestPrams", 'RN');
        post(Constants.test.api)(formData)().then(result => {
            setMsg(JSON.stringify(result));
        }).catch(e => {
            console.log(e);
            setMsg(JSON.stringify(e));
        })
    }
    return (
        <SafeAreaView>
            <TouchableOpacity onPress={doFetch}>
                <Text>加载</Text>
            </TouchableOpacity>
            <Text>{msg}</Text>
        </SafeAreaView>
    );
};
```

从上述代码中我们不难看出，在React Native中使用`State Hook`的主要步骤：

1. 导入`useState`：`import React, { useState } from 'react';`

2. 通过

   ```
   useState
   ```

   定义state：

   ```
   const [msg, setMsg] = useState('');
   ```

   - msg是定义的state中一个变量，**setMsg是用来修改msg变量的关联函数，它的格式是`set+变量名首字母大写`**

3. 修改状态：通过前面定义的关联函数`setMsg`修改即可`setMsg(JSON.stringify(result));`

4. `State Hook`的作用范围：因为Hooks只能应用与函数式组件，所以通过它声明的state的作用范围是函数内；

上面代码是摘自《[网络编程与数据存储技术](https://coding.imooc.com/class/304.html)》一章。

### 在React Native中使用 Effect Hook

Effect Hook 可以让你在函数组件中执行副作用操作。

我们可以把 useEffect Hook 看做React class 的生命周期函数：`componentDidMount`、`componentDidUpdate` 和 `componentWillUnmount` 这三个函数的组合。

> 需求2：假如我们需要在页面完成装载后的某个时刻执行某个操作，在页面卸载时执行一些清理会资源回收操作。

对于这样的一个需求对应的class代码如下：

```js
import React from 'react';
import {
    SafeAreaView,
    StyleSheet,
    Text,
    TouchableOpacity
} from 'react-native';
import Constants from './expand/dao/Constants';
import { post } from './expand/dao/HiNet';
export default class HiNetDemo extends React.Component<{}, { msg: string }> {
    timer: any;
    constructor(props: any) {
        super(props);
        this.state = {
            msg: ''
        }

    }
    componentDidMount() {
        this.timer = setTimeout(() => {
            this.doFetch();
        }, 2000);
    }
    componentWillUnmount() {
        this.timer && clearTimeout(this.timer);
    }
    doFetch = () => {
        const formData = new FormData();
        formData.append("requestPrams", 'RN');
        post(Constants.test.api)(formData)().then(result => {
            this.setState({
                msg: JSON.stringify(result)
            });
        }).catch(e => {
            console.log(e);
            this.setState({
                msg: JSON.stringify(e)
            });
        })
    }
    render() {
        return (
            <SafeAreaView>
                <TouchableOpacity onPress={this.doFetch}>
                    <Text>加载</Text>
                </TouchableOpacity>
                <Text>{this.state.msg}</Text>
            </SafeAreaView>
        );
    }
}
```

- 在上述代码中我们在`componentDidMount`通过定时器实现了当页面完成装载后2s发起了网络请求；
- 并在页面卸载时清空了计时器以防止内存泄漏；

那么，上述功能用Effect Hook又该如何实现呢？

还是以《[网络编程与数据存储技术](https://coding.imooc.com/class/304.html)》一章的网络编程一节为原型我们用Hooks来实现上述需求：

```js
import React, { useState, useEffect } from 'react';
import {
    SafeAreaView,
    StyleSheet,
    Text,
    TouchableOpacity
} from 'react-native';
import Constants from './expand/dao/Constants';
import { post } from './expand/dao/HiNet';
export default (props: { navigation: any }) => {
    const [msg, setMsg] = useState('');
    useEffect(() => {
        //对应componentDidUpdate
        function handleStatusChange(status: any) {
            console.log(status);
        }
        const timer = setTimeout(() => {
            doFetch();
        }, 2000);
        // 对应componentWillUnmount
        return function cleanup() {
            timer && clearTimeout(timer);
        };
    });
    const doFetch = () => {
        const formData = new FormData();
        formData.append("requestPrams", 'RN');
        post(Constants.test.api)(formData)().then(result => {
            setMsg(JSON.stringify(result));
        }).catch(e => {
            console.log(e);
            setMsg(JSON.stringify(e));
        })
    }
    return (
        <SafeAreaView>
            <TouchableOpacity onPress={doFetch}>
                <Text>加载</Text>
            </TouchableOpacity>
            <Text>{msg}</Text>
        </SafeAreaView>
    );
};
```

在上述代码中我们借助`useEffect`实现了class相同的功能，接下来我们来总结下在RN中使用Effect Hook的关键点：

1. 导入`useEffect`：`import React, { useState,useEffect } from 'react';`

2. 使用

   ```
   useEffect
   ```

   来实现不同生命周期函数的hooks：

   - 直接写在`useEffect(() => {}`一层的会在组件装载时调用，对应componentDidMount
   - `handleStatusChange`对应`componentDidUpdate`
   - `cleanup`对应`componentWillUnmount`在组件卸载时调用

## Hooks与class的选择

最后跟小伙伴们聊一聊什么时候该用Hooks？什么时候该用class？

- Hooks能够实现的class也都能实现
- 对于页面级等比较大的模块建议用class
- 对应组件级别比如封装一个按钮组件适合用Hooks

## 更多资料

- [Hooks官方文档](https://zh-hans.reactjs.org/docs/hooks-intro.html)