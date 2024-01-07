# React Native开发之React基础

## 

为了帮助大家快速上手React Native开发，在这本节中将向大家介绍开发React Native所需要的[一些React必备基础知识](https://coding.imooc.com/class/304.html?mc_marking=911b955aff9c2cfc95f12d0f15e1b2e7&mc_channel=shouji)。

## [概述](http://coding.imooc.com/class/304.html)

本节课将从React的特点、如何使用React、JSX语法，然后会对组件(Component）以及组件的属性(props)、状态(state)、生命周期等方面进行讲解。

### [通过本节课程能学到什么？](http://coding.imooc.com/class/304.html)

- 对React有个全面的认识；
- 熟悉JSX基本语法；
- 了解组件结构；
- 熟悉组件的生命周期；
- 学会使用props；
- 学会使用state；
- 熟悉自定义组件；

## [React是什么？](http://coding.imooc.com/class/304.html)

React 是 Facebook 推出的开源 JavaScript Library，它是一个用于组建用户界面的JavaScript库，让你以更简单的方式来创建交互式用户界面，它的出现让许多革新性的 Web 观念开始流行起来，例如：Virtual DOM、Component，声明式渲染等。

> 声明式与命令式

```
命令式编程：命令“机器”如何去做事情(how)，这样不管你想要的是什么(what)，它都会按照你的命令实现。
声明式编程：告诉“机器”你想要的是什么(what)，让机器想出如何去做(how)。
```

[演示](https://codepen.io/crazycodeboy/pen/VVJLYm?editors=0010)

1. 当数据改变时，React将高效的更新和渲染需要更新的组件。声明式视图使你的代码更可预测，更容易调试。
2. 构建封装管理自己的状态的组件，然后将它们组装成复杂的用户界面。由于组件逻辑是用JavaScript编写的，而不是模板，所以你可以轻松地通过您的应用程序传递丰富的数据，并保持DOM状态。
3. 一次学习随处可写，学习React，你不仅可以将它用于Web开发，也可以用于React Native来开发Android和iOS应用。

## [如何使用？](http://coding.imooc.com/class/304.html)

构建一个新的 React 单页应用，可以通过[Create React App](https://github.com/facebook/create-react-app)来完成。它可以帮助你配置开发环境，以便你可以使用最新的 JavaScript 特性，还能提供一个友好的开发体验，并为生产环境优化你的应用。

```
npm install -g create-react-app
create-react-app my-app
cd my-app
npm start
"dependencies": {
    "react": "^16.6.3",//是 React 的核心库
    "react-dom": "^16.6.3",//提供与 DOM 相关的功能
    "react-scripts": "2.1.1"//create-react-app 的一个核心包，一些脚本和工具的默认配置都集成在里面
  },
```

### [ReactDOM.render](http://coding.imooc.com/class/304.html)

> ReactDOM.render(element, container[, callback])

渲染一个 React 元素到由 container 提供的 DOM 中，并且返回组件的一个 引用(reference) （或者对于 无状态组件 返回 null ）。

## [JSX](http://coding.imooc.com/class/304.html)

JSX 是一个看起来很像 XML 的 JavaScript 语法扩展。 每一个XML标签都会被JSX转换工具转换成纯JavaScript代码，使用JSX，组件的结构和组件之间的关系看上去更加清晰。 JSX并不是React必须使用的，但React官方建议我们使用 JSX , 因为它能定义简洁且我们熟知的包含属性的树状结构语法。

**Usage:**

```
React.render(//使用JSX
    <div>
        <div>
            <div>content</div>
        </div>
    </div>,
    document.getElementById('example')
);
React.render(//不使用JSX
    React.createElement('div', null,
        React.createElement('div', null,
            React.createElement('div', null, 'content')
        )
    ),
    document.getElementById('example')
);
```

### [createElement](http://coding.imooc.com/class/304.html)

```
React.createElement(
  type,
  [props],
  [...children]
)
```

根据给定的类型创建并返回新的 React element 。参数type既可以是一个html标签名称字符串(例如’div’ 或 ‘span’ )，也可以是一个 React component 类型(一个类或一个函数)。

```
React.createElement(Hello, {toWhat: 'World'}, 'hello'),
//等价于 <Hello toWhat="World">hello</Hello>,
```

### [HTML标签 与 React组件 对比](http://coding.imooc.com/class/304.html)

React 可以渲染 HTML 标签 (strings) 或 React 组件 (classes)。 要渲染 HTML 标签，只需在 JSX 里使用小写字母开头的标签名。

```
var myDivElement = <div className="foo" />;
React.render(myDivElement, document.root);
```

要渲染 React 组件，只需创建一个大写字母开头的本地变量。

```
var MyComponent = ...;
var myElement = <MyComponent someProperty={true} />;
React.render(myElement, document.body);
```

> 提示：
>
> - React 的 JSX 里约定分别使用首字母大、小写来区分本地组件的类和 HTML 标签。
> - 由于 JSX 就是 JavaScript，一些标识符像 class 和 for 不建议作为 XML 属性名。作为替代， React DOM 使用 className 和 htmlFor 来做对应的属性。

### [JavaScript 表达式](http://coding.imooc.com/class/304.html)

#### [属性表达式](http://coding.imooc.com/class/304.html)

要使用 JavaScript 表达式作为属性值，只需把这个表达式用一对大括号 `{}` 包起来，不要用引号 `""`。

```
// 输入 (JSX):
var person = <Person name={window.isLoggedIn ? window.name : ''} />;
// 输出 (JS):
var person = React.createElement(
  Person,
  {name: window.isLoggedIn ? window.name : ''}
);
```

#### [子节点表达式](http://coding.imooc.com/class/304.html)

同样地，JavaScript 表达式可用于描述子结点：

```
// 输入 (JSX):
var content = <Container>{window.isLoggedIn ? <Nav /> : <Login />}</Container>;
// 输出 (JS):
var content = React.createElement(
  Container,
  null,
  window.isLoggedIn ? React.createElement(Nav) : React.createElement(Login)
);
```

### [注释](http://coding.imooc.com/class/304.html)

JSX 里添加注释很容易，它们只是 JS 表达式而已。你只需要在一个标签的子节点内(非最外层)用 {} 包围要注释的部分。

```
class ReactDemo extends Component {
  render() {
    return (
      <View style={styles.container}>
        {/*标签子节点的注释*/}
        <Text style={styles.welcome}
          //textAlign='right'
          textShadowColor='yellow'
          /*color='red'
          textShadowRadius='1'*/ >
          React Native!
        </Text>
      </View>
    );
  }
}
```

> 心得：在标签节点以外注释，和通常的注释是一样的，多行用“/**/” 单行用“//”；

### [JSX延展属性](http://coding.imooc.com/class/304.html)

#### [不要试图去修改组件的属性](http://coding.imooc.com/class/304.html)

不推荐做法：

```
  var component = <Component />;
  component.props.foo = x; // 不推荐
  component.props.bar = y; // 不推荐
```

这样修改组件的属性，会导致React不会对组件的属性类型（propTypes）进行的检查。从而引发一些预料之外的问题。

推荐做法：

```
var component = <Component foo={x} bar={y} />;
```

#### [延展属性（Spread Attributes）](http://coding.imooc.com/class/304.html)

你可以使用 JSX 的新特性 - 延展属性：

```
  var props = {};
  props.foo = x;
  props.bar = y;
  var component = <Component {...props} />;
```

传入对象的属性会被复制到组件内。

它能被多次使用，也可以和其它属性一起用。注意顺序很重要，后面的会覆盖掉前面的。

```
  var props = { foo: 'default' };
  var component = <Component {...props} foo={'override'} />;
  console.log(component.props.foo); // 'override'
```

上文出现的`...`标记被叫做延展操作符（spread operator）已经被 ES6 数组 支持。

> https://www.devio.org/2018/09/09/ES6-ES7-ES8-Feature/#14

## [Component](http://coding.imooc.com/class/304.html)

React 允许将代码封装成组件（component），然后像插入普通 HTML 标签一样，在网页中插入这个组件。

```
class Hello extends React.Component{
    render() {
        return <h1>Hello {this.props.name}</h1>;
    }
}
ReactDOM.render(
  <Hello name="John" />,
  document.getElementById('example')
);
```

上面代码中，变量 HelloMessage 就是一个组件类。模板插入 `<HelloMessage /> `时，会自动生成 HelloMessage 的一个实例。所有组件类都必须有自己的 render 方法，用于输出组件。

> 注意

- 组件类的第一个字母必须大写
- *组件类只能包含一个顶层标签?* [演示](https://codepen.io/crazycodeboy/pen/ZmdjMK?editors=0010)

## [组件的属性(props)](http://coding.imooc.com/class/304.html)

我们可以通过`this.props.xx`的形式获取组件对象的属性，对象的属性可以任意定义，但要避免与JavaScript关键字冲突。

### [遍历对象的属性：](http://coding.imooc.com/class/304.html)

`this.props.children`会返回组件对象的所有属性。 React 提供一个工具方法 React.Children 来处理 this.props.children 。我们可以用 `React.Children.map`或`React.Children.forEach` 来遍历子节点。

**React.Children.map**

```
React.Children.map(children, function[(thisArg)])
```

在包含在 children 里的每个子级上调用函数，调用的函数的 this 设置为 thisArg 。如果 children 是一个嵌套的对象或数组，它将被遍历。如果 children 是 null 或 undefined ，返回 null 或 undefined 而不是一个空数组。

**React.Children.forEach**

```
React.Children.forEach(children, function[(thisArg)])
```

**Usage：**

```
class NotesList extends React.Component{
    render(){
        return (
            <ol>
                {
                    React.Children.map(this.props.children,(child)=> {
                        return <h1>{child}</h1>;                     })
                }
            </ol>         );
    }
}
ReactDOM.render(<NotesList>
    <span>hello</span>     <span>world</span> </NotesList>, document.getElementById('root'));
```

[演示](https://codepen.io/crazycodeboy/pen/EOBpzE?editors=0010)

### [[PropTypes\]](http://coding.imooc.com/class/304.html)

组件的属性可以接受任意值，字符串、对象、函数等等都可以。有时，我们需要一种机制，验证别人使用组件时，提供的参数是否符合要求。 组件类的PropTypes属性，就是用来验证组件实例的属性是否符合要求。

> React.PropTypes 从 React v15.5开始被移入了`prop-types`，使用时需要留意；

```
import  PropTypes from 'prop-types'
class MyTitle extends React.Component{
    static propTypes={
        title: PropTypes.string.isRequired,
    };
    render() {
        return <h1> title:{this.props.title} </h1>;
    }
}
ReactDOM.render(<MyTitle />, document.getElementById('root'));
```

上面的Mytitle组件有一个title属性。PropTypes 告诉 React，这个 title 属性是必须的，而且它的值必须是字符串。现在，我们设置 title 属性的值是一个数值。

```
var data = 123;
ReactDOM.render(
  <MyTitle title={data} />,
  document.body
);
```

这样一来，title属性就通不过验证了。控制台会显示一行错误信息。

```
Warning: Failed propType: Invalid prop `title` of type `number` supplied to `MyTitle`, expected `string`.
```

更多的PropTypes设置，可以查看[官方文档](https://reactjs.org/docs/typechecking-with-proptypes.html#proptypes)。

### [默认属性](http://coding.imooc.com/class/304.html)

此外，可以通过defaultProps用来设置组件属性的默认值。

```
class MyTitle extends React.Component{
    static defaultProps={
        shortName:'MyTitle'
    };
    render() {
        return <h1> {this.props.shortName}</h1>;
    }
}
ReactDOM.render(<MyTitle/>, document.getElementById('root'));
```

上面代码会输出`"MyTitle"`。

### [ref 属性(获取真实的DOM节点)](http://coding.imooc.com/class/304.html)

组件并不是真实的 DOM 节点，而是存在于内存之中的一种数据结构，叫做虚拟 DOM （virtual DOM）。只有当它插入文档以后，才会变成真实的 DOM 。根据 React 的设计，所有的 DOM 变动，都先在虚拟 DOM 上发生，然后再将实际发生变动的部分，反映在真实 DOM上，这种算法叫做 DOM diff ，它可以极大提高网页的性能表现。

但是，有时需要从组件获取真实 DOM 的节点，这时就要用到 ref 属性。

```
class Alert extends React.Component {
    showAlert(message) {
        alert(`Debug:${message}`);
    }

    render() {
        return null;
    }
}

class MyTitle extends React.Component {
    onClick = () => {
        this.refs.alert.showAlert('MyTitle');
    };

    render() {
        return <div>
            <h1 onClick={this.onClick}>Click me</h1>
            <Alert ref='alert'/>
        </div>;
    }
}

ReactDOM.render(<MyTitle/>, document.getElementById('root'));
```

上面代码中，组件 MyTitle 的子节点有一个Alert组件，为了调用这个组件提供的方法，这时就必须获取真实的 DOM 节点，虚拟 DOM 是拿不到用户输入的。为了做到这一点，我们在使用这个组件的时候必须为其设置一个ref属性，然后 this.refs.[refName] 就会返回这个真实的 DOM 节点。

需要注意的是，由于 this.refs.[refName] 属性获取的是真实 DOM ，所以必须等到虚拟 DOM 插入文档以后，才能使用这个属性，否则会报错。上面代码中，通过为组件指定 Click 事件的回调函数，确保了只有等到真实 DOM 发生 Click 事件之后，才会读取 this.refs.[refName] 属性。

React 组件支持很多事件，除了 Click 事件以外，还有 KeyDown 、Copy、Scroll 等，完整的事件清单请查看[官方文档](https://facebook.github.io/react/docs/events.html#supported-events)。

> 心得：ref属性在开发中使用频率很高，使用它你可以获取到任何你想要获取的组件的对象，有了这个对象你就可以灵活地做很多事情，比如：读写对象的变量，甚至调用对象的函数。

## [state](http://coding.imooc.com/class/304.html)

上文讲到了props，组件会根据props的变化来进行渲染，但组件无法改变自身的props，那么组件为了实现交互，可以使用组件的 state 。state 是组件私有的，可以通过state={}方式初始化，通过调用 `this.setState()` 来改变它。当 state 更新之后，组件就会重新渲染自己。

render() 方法依赖于 this.props 和 this.state ，框架会确保渲染出来的 UI 界面总是与输入（ this.props 和 this.state ）保持一致。

### [初始化state](http://coding.imooc.com/class/304.html)

可以通过一下两种方式来初始化state，在组件的生命周期中仅执行一次，用于设置组件的初始化 state 。

```
constructor(props){
    super(props);
    this.state={
        name:''
    }
}
//or
state={
    name:''
}
```

### [更新 state](http://coding.imooc.com/class/304.html)

通过`this.setState()`方法来更新state，调用该方法后，React会重新渲染相关的UI。`this.setState({favorite:!this.state.favorite});`

**Usage:**

```
class FavoriteButton extends React.Component{
   state={
       favorite:false
   };
    handleClick=()=>{
        this.setState({favorite:!this.state.favorite});
    };
    render(){
        const text=this.state.favorite? 'favorite':'un favorite';
        return (
            <h1 onClick={this.handleClick}>
                You {text} this. Click to toggle.
            </h1>         );
    }
}
```

上面代码是一个 FavoriteButton 组件，它的通过 state={}初始状态，也就是一个对象，这个对象可以通过 this.state 属性读取。当用户点击组件，导致状态变化，this.setState 方法就修改状态值，每次修改以后，自动调用 this.render 方法，再次渲染组件。

> 心得：由于 this.props 和 this.state 都用于描述组件的特性，可能会产生混淆。一个简单的区分方法是，this.props 表示那些本组件无法改变的特性，而 this.state 是会随着用户互动而产生变化的特性。

## [组件的生命周期](http://coding.imooc.com/class/304.html)

在iOS中`UIViewController`提供了`(void)viewWillAppear:(BOOL)animated`, `- (void)viewDidLoad`,`(void)viewWillDisappear:(BOOL)animated`等生命周期方法，在Android中`Activity`则提供了` onCreate()`,`onStart()`,`onResume()`,`onPause()`,`onStop()`,`onDestroy()`等生命周期方法，这些生命周期方法描述了一个界面从创建到销毁的一生。

那么在React 中组件(Component)也是有自己的生命周期方法的。

[![react-lifecycle-methods-diagram](https://img.alicdn.com/tfs/TB1ELaIugHqK1RjSZJnXXbNLpXa-1093-618.png)](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

[演示](https://codepen.io/crazycodeboy/pen/oQKvJZ?editors=0011)

### [组件的生命周期分成三个时期：

- Mounting：创建时
- Updating：更新时
- Unmounting：卸载时

### [不安全的方法](http://coding.imooc.com/class/304.html)

- componentWillMount
- componentWillReceiveProps
- componentWillUpdate

使用这些生命周期方法通常会导致错误和不一致，因此将来会被弃用。在新的React版本中他们被标记为UNSAFE。

> [static-lifecycle-methods](https://github.com/reactjs/rfcs/blob/master/text/0006-static-lifecycle-methods.md)

### [Mounting(装载)](http://coding.imooc.com/class/304.html)

- [constructor()](https://www.devio.org/2019/03/03/react-basis-for-react-native/#constructor)；
- [static getDerivedStateFromProps()](https://www.devio.org/2019/03/03/react-basis-for-react-native/#static-getderivedstatefromprops)
- [render()](https://www.devio.org/2019/03/03/react-basis-for-react-native/#render)
- [componentDidMount()](https://www.devio.org/2019/03/03/react-basis-for-react-native/#componentdidmount)

#### [constructor()](http://coding.imooc.com/class/304.html)

```
constructor(props)
```

React组件的构造函数将会在装配之前被调用。当为一个React.Component子类定义构造函数时，你应该在任何其他的表达式之前调用super(props)。否则，this.props在构造函数中将是未定义，并可能引发异常。

> 构造函数是初始化状态的合适位置。若你不初始化状态且不绑定方法，那你也不需要为你的React组件定义一个构造函数。

#### [static getDerivedStateFromProps()](http://coding.imooc.com/class/304.html)

```
static getDerivedStateFromProps(nextProps, prevState)
```

组件实例化后和接受新属性时将会调用getDerivedStateFromProps。它应该返回一个对象来更新状态，或者返回null来表明新属性不需要更新任何状态。

注意，如果父组件导致了组件的重新渲染，即使属性没有更新，这一方法也会被调用。如果你只想处理变化，那么可以通过比较新旧值来完成。

> 调用this.setState() 通常不会触发 getDerivedStateFromProps()。

#### [render](http://coding.imooc.com/class/304.html)

```
ReactComponent render()
```

`render()` 方法是必须的。

当被调用时，其会检查this.props 和 this.state并返回以下类型中的一个:

- React元素。 通常是由 JSX 创建。该元素可能是一个原生DOM组件的表示，如<div />，或者是一个你定义的复合组件。
- 字符串和数字。 这些将被渲染为 DOM 中的 text node。
- Portals。 由 [ReactDOM.createPortal](https://react.docschina.org/docs/portals.html) 创建。
- null。 什么都不渲染。
- 布尔值。 什么都不渲染。（通常存在于 return test && 写法，其中 test 是布尔值。）

返回null 或 false时，ReactDOM.findDOMNode(this) 将返回 null。

> `render() `函数应该是纯粹的，也就是说该函数不修改组件的 `state`，每次调用都返回相同的结果，不读写 DOM 信息，也不和浏览器交互（例如通过使用 `setTimeout`）。如果需要和浏览器交互，在 `componentDidMount()` 中或者其它生命周期方法中做这件事。保持 `render()` 纯粹，可以使服务器端渲染更加切实可行，也使组件更容易被理解。

> 提示：若 shouldComponentUpdate()返回false，render()函数将不会被调用。

#### [componentDidMount()](http://coding.imooc.com/class/304.html)

```
componentDidMount()
```

componentDidMount()在组件被装配后立即调用，通常在该方法中进行一些初始化操作。·初始化时需要DOM节点的操作可以放到这里进行`。若你需要从远端加载数据，这是一个适合实现网络请求的地方。在该方法里设置状态将会触发重渲。

> 这一方法是一个发起任何订阅的好地方。如果你这么做了，别忘了在componentWillUnmount()退订。

另外，在这个方法中调用setState()将会触发一次额外的渲染，但是它将在浏览器刷新屏幕之前发生。这保证了即使render()将会调用两次，但用户不会看到中间状态。

### [Updating (更新)](http://coding.imooc.com/class/304.html)

- [static getDerivedStateFromProps()](https://www.devio.org/2019/03/03/react-basis-for-react-native/#static-getderivedstatefromprops)
- [shouldComponentUpdate](https://www.devio.org/2019/03/03/react-basis-for-react-native/#shouldcomponentupdate)
- [render()](https://www.devio.org/2019/03/03/react-basis-for-react-native/#render)
- [getSnapshotBeforeUpdate()](https://www.devio.org/2019/03/03/react-basis-for-react-native/#getsnapshotbeforeupdate)
- [componentDidUpdate](https://www.devio.org/2019/03/03/react-basis-for-react-native/#componentdidupdate)

#### [shouldComponentUpdate](http://coding.imooc.com/class/304.html)

```
shouldComponentUpdate(nextProps, nextState)
```

在接收到新的 props 或者 state，将要渲染之前调用，以让React知道当前状态或属性的改变是否不影响组件的输出。

该方法在初始化渲染的时候不会调用，在使用 forceUpdate 方法的时候也不会。如果确定新的 props 和 state 不需要重新渲染，则此处应该 返回 false。

> 心得：重写次方你可以根据实际情况，来灵活的控制组件当 props 和 state 发生变化时是否要重新渲染组件。

#### [getSnapshotBeforeUpdate](http://coding.imooc.com/class/304.html)

```
getSnapshotBeforeUpdate(prevProps, prevState)
```

getSnapshotBeforeUpdate()在最新的渲染输出提交给DOM前将会立即调用。它让你的组件能在当前的值可能要改变前获得它们。这一生命周期返回的任何值将会 作为参数被传递给componentDidUpdate()。

#### [componentDidUpdate](http://coding.imooc.com/class/304.html)

```
componentDidUpdate(prevProps, prevState, snapshot)
```

在组件的更新已经同步到 DOM 中之后立刻被调用。

> 该方法不会在初始化渲染的时候调用。使用该方法可以在组件更新之后操作 DOM 元素。

### [Unmounting(移除)](http://coding.imooc.com/class/304.html)

#### [componentWillUnmount](http://coding.imooc.com/class/304.html)

```
componentWillUnmount()
```

在组件从 DOM 中移除的时候立刻被调用。

在该方法中执行任何必要的清理，比如无效的定时器，或者清除在 componentDidMount 中创建的 DOM 元素。

## [参考](http://coding.imooc.com/class/304.html)

- [新版React Native+Redux打造高质量上线App](http://coding.imooc.com/class/304.html)
- [ES6、ES7、ES8特性一锅炖](https://www.devio.org/2018/09/09/ES6-ES7-ES8-Feature/)
- [reactjs](https://reactjs.org/)
- [react-lifecycle-methods-diagram](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)