[toc]

----

# React Native 中组件的生命周期



> [劉光軍_Shine](https://www.jianshu.com/u/5ef2046ade86)关注
2017.11.03 17:34:38字数 1,672阅读 1,582

### React Native组件执行顺序介绍





类似于iOS的生命周期，iOS中有loadView/nib->viewDidLoad->viewWillAppear->viewDidAppear->viewWillDisappear->viewDidDisappear(->didReceiveMemoryWarning)->viewDidUnload，在React Native中是怎么表现的呢？通过一张图来说明：

![9159664-fd1486211b47307d](images/9159664-fd1486211b47307d.jpg)

react-native生命周期.jpg



从图上看，上班部分属于实例化阶段，左边属于存在阶段，右边属于销毁阶段。所以从这张生命周期图中，我们可以看出，在React Native中，组件的生命周期大致可以分为3个阶段（实例化阶段，存在阶段，销毁阶段），其中最常接触的为实例化阶段，这个阶段负责组件的构建和展示的时间，需要我们根据几个函数的调用过程，控制好组件的展示和逻辑处理。

##### 实例化阶段函数功能分析

- ***大多数组件在创建时就可以使用各种参数来进行定制，用于定制的这些参数就成为属性（props）\***
  - getDefaultProps：，该函数用于初始化一些默认属性，通常会将固定的内容放在这个函数中进行初始化和赋值。
    - 在组件中，我们可以利用this.props获取在这里初始化它的属性，由于组件初始化后，再次使用该组件不会调用getDefaultProps函数，所以组件自己不可以修改props，只可由其他组件调用它时再外部进行修改。
- ***对于需要在该指定的组件生命周期中改变的数据我们使用state\***
  - getInitialState：该函数用于对组件一些状态进行初始化
    - 该函数不同于getDefaultProps,在以后的过程中，会再次调用，所以可以将控制控件状态的一些变量放在这里初始化，比如控件上显示的文字，可以通过this.state来获取值，通过this.setState来修改state值。***注意：一旦调用了this.setState方法，组件一定会调用render方法，对组件进行再次渲染，不过，React框架会根据DOM的状态自动判断是否需要真正渲染\***
- componentWillMount:相当于OC中的viewWillAppear方法，在组件将要被加载到视图之前调用。
- render：它是每个组件必需具备的方法，本质上是个函数，并且返回JSX或者其他组件来构成DOM，和Android的XML布局类似。
  - 在该函数中，只能通过this.state和this.props来访问之前在函数中初始化的数值
  - 只能返回一个顶级元素
- componentDidMount:在调用了render方法，组件加载成功并被成功渲染出来之后，所要执行的后续操作，一般都会在这个函数中进行，比如经常要面对的网络请求等加载数据操作
  - 因为UI已经成功渲染，而且这里面是异步的，所以放在这个函数进行数据的请求等复杂的操作，不会出现UI错误。（和iOS的viewDidLoad类似？感觉像但是也不像）

##### 存在阶段函数功能分析

- componentWillReceiveProps:指父元素对组件的props或state进行了修改
- shouldComponentUpdate:一般用于优化，可以返回false或true来控制是否进行渲染
- componentWillUpdate:组件刷新前调用，类似：componentWillMount
- componentDidUpdate：更新后的hook

##### 销毁阶段函数功能分析

- 用于清理一些无用的内容，比如：点击事件Listener,只有一个过程：componentWillUnmount

##### 常用知识点分析

- this.state:开发中，组件肯定要与用户进行交互，React的一大创新就是将组件看成了一个状态机，一开始有一个初始状态，然后用户交互，导致状态变化，从而触发重新渲染UI
  - 当用户点击组件，导致状态变化，this.setSate方法就修改状态值，每次修改以后，会自动调用this.render方法，再次渲染组件。
  - 可以把组件看成一个状态机，根据不同的status有不同的UI展示，只要使用setState改变状态值，根据diff算法算出有差值后，就会执行ReactDom的render方法，重新渲染界面。
  - 注意：由于this.props和this.state都用于描述组件的特性，可能会产生混淆，一个简单的区分方法就是---this.props表示那些一旦定义，就不再更改的特性，而this.state是会随着用户交互而产生改变的特性。
- 获取真实的Dom节点
  - 在React Native中，组件并不是真实的DOM节点，而是存在于内存中的一种数据结构，叫虚拟DOM
  - 只有当它插入文档后，才会变成真实的DOM
  - 根据React的设计，所有DOM变动，都现在虚拟DOM上发生，然后再将实际发生变动的部分，反映在真实DOM上，这种算法叫做DOM diff，它可以极大提高网页的性能表现。
  - 有时需要从组建获取真实DOM节点，这时就需要到ref属性。

***什么是DOM diff算法\***

- Web界面由DOM树来构成，当其中某一部分发生变化时，其实就是对应的某个DOM节点发生了变化，在React中，构建UI界面的思路是由当前状态决定界面，前后两个状态就对应两套界面，然后由React来比较两个界面的区别，这就需要对DOM树进行Diff算法分析。
- 即给定任意两棵树，找到最少的转换步骤。但是标准的的Diff算法复杂度需要O(n^3)，这显然无法满足性能要求。要达到每次界面都可以整体刷新界面的目的，势必需要对算法进行优化。这看上去非常有难度，然而Facebook工程师却做到了，他们结合Web界面的特点做出了两个简单的假设，使得Diff算法复杂度直接降低到O(n)
  - 两个相同组件产生类似的DOM结构，不同的组件产生不同的DOM结构
  - 对于同一层次的一组子节点，它们可以通过唯一的id进行区分
    -算法上的优化是React整个界面Render的基础，事实也证明这两个假设是合理而精确的，保证了整体界面构建的性能



1人点赞



[ReactNative学习笔记](https://www.jianshu.com/nb/18423769)