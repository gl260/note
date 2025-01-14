在react当中 不要去直接修改this.state中的数据

```js
constructor() {
  super();
  this.state = {
    books: books,
  };
}
changeCount(index, num) {
  // 不要直接去修改原来的数据 - 先浅结构一下
  const newBooks = [...this.state.books];
  newBooks[index].count += num;
  this.setState({ books: newBooks });
}
```

一旦执行setState render函数就会重新执行

Vue里面也是有这样做的 只不过Vue是将数据劫持了 就会自动帮我们执行render

react中需要我们显示的调用setState

## 1. React基础

### 1.1 什么是React? 说说你对React的理解

* React是RaceBook在2013年开源的JavaScript框架
* 是用于构建用户界面的 JavaScript 库
* 遵循 `组件化开发`、`声明式编程范式`和`函数式编程`概念，使前端应用程序更高效
* 如今React和Vue是国内最为流行的两个前端框架, 都是帮我们构建用户界面的JavaScript库

##### React特性

* JSX 语法
* 单向数据绑定
* 虚拟 DOM
* 声明式编程 -- 声明式编程是一种编程范式，它关注的是你要做什么，而不是如何做
* Component -- 在React中, 一切皆为组件
  * 一个组件该有的特点如下：
    * 可组合：每个组件易于和其它组件一起使用，或者嵌套在另一个组件内部
    * 可重用：每个组件都是具有独立功能的，它可以被使用在多个 UI 场景
    * 可维护：每个小的组件仅仅包含自身的逻辑，更容易被理解和维护

##### 优势

* 高效灵活
* 声明式的设计，简单使用
* 组件化开发，提高代码复用率
* 单向响应的数据流会比双向绑定的更安全，速度更快





### 1.2 React的特点

##### 官网说的三点

* 声明式
  * 声明式编程目前是整个前端的开发模式 : Vue React Flutter等
  * 它允许我们只需要维护自己的状态,当状态发生改变时,React会根据最新的状态来渲染UI界面
* 组件化
  * 组件化开发也是目前前端开发的趋势,就是将页面拆分成一个个小的组件
* 跨平台
  * ReactNative，用于开发移动端跨平台
  * ReactVR，用于开发虚拟现实Web应用程序





### 1.3 什么是jsx?

* JSX是⼀种JavaScript的语法扩展
* 它用于描述我们的UI界面，并且可以和JavaScript融合在一起使用
* 它不同于Vue中的模块语法，我们不需要专门学习模板语法中的一些指令（比如v-for、v-if、v-else、v-bind）





### 1.4 JSX转换的本质是什么?

* jsx是通过babel工具转换编译成React代码的
* 本质
  - jsx 仅仅只是 React.createElement(component, props, ...children) 函数的语法糖
  - 所有的jsx最终都会被转换成React.createElement的函数调用





### 1.5 为什么React选择了JSX





### 1.6 React为什么采用虚拟DOM?

* 操作真实DOM性能较低: 一个最简单的div也包含着很多属性,操作DOM的代价是非常昂贵的
* 虚拟DOM帮助我们从命令式编程转向声明式编程
* 虚拟DOM带来了跨平台的能力





### 1.7 React事件函数绑定this有几种方式?

* this绑定规则

  - 普通绑定 - `onClick={this.btnClick}` - 在内部是独立函数调用,所以this为undefined
  - this绑定方式一: bind绑定 - `onClick={this.btnClick.bind(this)}`
  - this绑定方式二: ES6 class fields - `onClick={this.btnClick}` - `btnClick = () => {}`
  - this绑定方式三: 直接传入一个箭头函数 - `onClick={() => this.btnClick()}`

* 给函数传递参

  - event参数的传递 - `onClick={(event) => this.btn1Click(event)}`
  - 额外参数的传递 - `onClick={(event) => this.btn2Click(event, "http", 18)}`

  ```js
  btn1Click(event) {
    console.log(event);
  }
  btn2Click(event, name, age) {
    console.log(event, name, age);
  }
  ```

  



### 1.8 说说事件参数如何传递参数?

* 上面1.7





### 1.9 React事件和普通的HTML事件有什么不同?

* 





### 1.10 什么是高价函数? 什么是高阶HOC组件?

高阶函数: 至少满足一下条件之一    -- filter、map、reduce都是高阶函数

* 接收一个或者多个函数作为输入
* 输出一个函数

高阶组件: Higher-Order Components，简称为 HOC

* 高阶组件是参数为组件，返回值为新组件的函数 -- 就是传入一个组件,对这个组件进行一些功能的增强,在返回出来新的组件
* 注意: 首先 高阶组件 本身不是一个组件，而是一个函数 其次，这个函数的参数是一个组件，返回值也是一个组件





### 1.11 说说高阶组件的应用场景?





### 1.12 React如何创建Refs来获取对应的DOM呢?

* 方式一: 在react元素上绑定ref字符串 - 这种方式react已经不推荐了
  * 使⽤时通过 `this.refs.传入的字符串` 格式获取对应的元素
* 方式二: 提前创建好ref对象, createRef(), 将创建出来的对象绑定到元素(推荐)
  * 对象是通过 `React.createRef()` 方式创建出来的
* 方式三: 传入一个回调函数, 在对应的元素被渲染之后, 回调函数被执行, 并且将元素传入(16.3之前的版本)

```js
import React, { PureComponent, createRef } from 'react'

export class App extends PureComponent {
  constructor() {
    super()
    this.state = {}
    this.titleRef = createRef()
    this.titleEl = null
  }
  getDOM() {
    // 方式一: 在react元素上绑定ref字符串 - 这种方式react已经不推荐了
    // console.log(this.refs.http)

    // 方式二: 提前创建好ref对象, createRef(), 将创建出来的对象绑定到元素(推荐)
    // console.log(this.titleRef.current)

    // 方式三: 传入一个回调函数, 在对应的元素被渲染之后, 回调函数被执行, 并且将元素传入(16.3之前的版本)
    console.log(this.titleEl)
  }
  render() {
    return (
      <div>
        <h3 ref="http">大大怪将军</h3>
        <h3 ref={this.titleRef}>小小怪下士</h3>
        <h3 ref={el => this.titleEl = el}>瑞克</h3>
        <button onClick={() => this.getDOM()}>获取DOM</button>
      </div>
    )
  }
}

export default App
```







### 1.13 说说你对React context的理解

在React中，数据传递⼀般使用props传递数据，维持单向数据流，这样可以让组件之间的关系变得简单且可预测，但是单项数据流在某些场景中并不适用。单纯一对父子组件传递并无问题，但要是组件之间层层依赖深入，props就需要层层传递显然，这样做太繁琐了。

Context 提供了一种在组件之间共享此类值的方式，而不必显式地通过组件树的逐层传递 props

**简单说就是，当你不想在组件树中通过逐层传递props或者state的方式来传递数据时，可以使用Context来实现跨层级的组件数据传递。**

JS的代码块在执⾏期间，会创建⼀个相应的作⽤域链，这个作⽤域链记录着运⾏时JS代码块执⾏期间所能访问的活动对象，包括变量和函数，JS程序通过作⽤域链访问到代码块内部或者外部的变量和函数。

假如以JS的作用域链作为类比，React组件提供的Context对象其实就好比一个提供给子组件访问的作用域，而Context对象的属性可以看成作用域上的活动对象。由于组件 的 Context 由其父节点链上所有组件通 过getChildContext（）返回的Context对象组合而成，所以，组件通过Context是可以访问到其父组件链上所有节点组件提供的Context的属性。





### 1.14 类组件与函数组件有什么异同?





### 1.15 React重要的组件生命周期有哪些？分别列出他们的作用。

- constructor() - 在 React 组件挂载之前，会调用它的构造函数。
- render() - 是 class 组件中唯一必须实现的方法。
- componentDidMount() - 组件已经挂载到DOM树上时 立即调用。
- componentDidUpdate() - 在更新后会被立即调用。首次渲染不会执行此方法。
- componentWillUnmount() - 在组件卸载及销毁之前直接调用。



### 1.16 React的setState是同步的还是异步的？React18中是怎么样的？

* 在 React 中，可变状态通常保存在组件的 state 属性中，并且只能通过使用 setState()来更新

* React的setState是异步的 -- 不要指望在调用 `setState` 之后，`this.state` 会立即映射为新的值

* 在react18之前, 在setTimeout,Promise等中操作setState, 是同步操作

* 在react18之后, 在setTimeout,Promise等中setState异步操作(批处理)

  - 如果需要同步的处理怎么办呢? 需要执行特殊的`flushSync`操作
  - 为什么要将setState设计成异步的
  - 首先,若是将setState设计成同步的,在`componentDidMount`中请求多个网络请求时,会堵塞后面的网络请求

  ```js
  componentDidMount() {
    // 网络请求一 : this.setState
    // 网络请求二 : this.setState
    // 网络请求三 : this.setState
    // 如果this.setState设计成同步的,会堵塞后面的网络请求
  }
  ```

  - 一. setState设计为异步，可以显著的提升性能

    - 如果每次调用 setState都进行一次更新，那么意味着render函数会被频繁调用，界面重新渲染，这样效率是很低的
    - 最好的办法应该是**获取到多个更新，之后进行批量更新**

    ```js
    // 在一个函数中有多个setState时,
    this.setState({}) --> 先不会更新,而是会加入到队列(queue)中 (先进先出)
    this.setState({}) --> 也加入到队列中
    this.setState({}) --> 也加入到队列中
    // 这里的三个setState会被合并到队列中去
    // 在源码内部是通过do...while从队列中取出依次执行的
    ```

  - 二: 如果同步更新了state，但是还没有执行render函数，那么state和props不能保持同步



### 1.17 性能优化:什么是SCU优化？类组件和函数组件分别如何进行SCU的优化？

- **shouldComponentUpdate -- SCU** -- React提供给我们的声明周期方法

- SCU优化就是 一种巧妙的技术,用来减少DOM操作次数,具体为当React元素没有更新时,不会去调用render()方法

- 可以通过`shouldComponentUpdate`来判断`this.state`中的值是否改变

  ```js
  shouldComponentUpdate(nextProps, nextState) {
     const {message, counter} = this.state
     if(message !== nextState.message || counter !== nextState.counter) {
       return true
     }
     return false 
   }
  ```

- React已经帮我们提供好SCU优化的操作

  - 类组件: 将class继承自`PureComponent`
  - 函数组件: 使用一个高阶组件`memo`

  ```js
  import {mome} from 'react'
  
  const HomeFunc = mome(function(props) {
    console.log("函数式组件")
    return (
      <h4>函数式组件: {props.message}</h4>
    )
  })
  
  export default HomeFunc
  ```





### 1.18 性能优化:React的diff算法和key的作用

- React的渲染流程

  - 在render函数中返回jsx, jsx会创建出`ReactElement`对象(通过React.createElement的函数创建出来的)
  - `ReactElement`最终会形成一颗树结构, 这颗树结构就是vDOM
  - React会根据这样的vDOM渲染出真实DOM

- React更新流程

  - props/state发生改变
  - render函数重新执行
  - 产生新的DOM树结构
  - 新旧DOM树 进行diff算法
  - 计算出差异进行更新
  - 最后更新到真实DOM

  ```js
  什么是diff算法?
      diff算法并非React独家首创,但是React针对diff算法做了自己的优化,使得时间复杂度优化成了O(n)
  对比两颗树结构,然后帮助我们计算出vDOM中真正变化的部分,并只针对该部分进行实际的DOM操作,而非渲染整个页面,从而保证了每次操作后页面的高效渲染。
  
  传统Diff算法是循环递归每一个节点
  将两颗树中所有的节点一一对比需要O(n²)的复杂度，在对比过程中发现旧节点在新的树中未找到，那么就需要把旧节点删除，删除一棵树的一个节点(找到一个合适的节点放到被删除的位置)的时间复杂度为O(n),同理添加新节点的复杂度也是O(n),合起来diff两个树的复杂度就是O(n³)
  ```

- React在props或state发生改变时，会调用React的render方法，会创建一颗不同的树

- React需要基于这两颗不同的树之间的差别来判断如何有效的更新UI

- 如果一棵树参考另外一棵树进行完全比较更新，那么即使是最先进的算法，该算法的**复杂程度为 O(n³)**，其中 n 是树中元素的数量

- 如果在 React 中使用了该算法，那么展示 1000 个元素所需要执行的计算量将在十亿的量级范围

- 这个开销太过昂贵了，于是，React对这个算法进行了优化，**将其优化成了O(n)**

  - 同层节点之间相互比较，不会垮节点比较(一旦某个节点不同,那么包括其后代节点都会被替换)

    ![Snipaste_2022-09-15_17-00-21](E:\Typora-文件\Typora图片位置\Snipaste_2022-09-15_17-00-21.png)

  - 不同类型的节点，产生不同的树结构(当根节点为不同类型的元素时，React 会拆卸原有的树并且建立起新的树)

  - 开发中，可以通过key属性标识哪些子元素在不同的渲染中可能是不变的

- 在遍历列表时，总是会提示一个警告，让我们加入一个key属性，当子元素拥有 key 时，React 使用 key 来匹配原有树上的子元素以及最新树上的子元素。

  - 在最后位置插入数据 -- 这种情况，有无key意义并不大
  - 在前面插入数据 -- 这种做法，在没有key的情况下，所有的li都需要进行修改
  - 在中间插入元素 -- 新增2014, key为2016元素仅仅进行位移，不需要进行任何的修改

  ```jsx
  <ul>
    <li key="2015">Duke</li>
    <li key="2016">Villanova</li>
  </ul>
  
  <ul>
    <li key="2015">Duke</li>
    <li key="2014">Connecticut</li>
    <li key="2016">Villanova</li>
  </ul>
  ```





## 2. React中编写CSS样式

- css内联样式

  ```js
  * 优点: 样式之间不会有冲突，可以动态获取当前state中的状态
  * 缺点: 大量编写内联样式导致代码混乱
  ```

- 普通的css写法

  ```js
  * App.css ---> 引入 import './App.css'
  * 这种方式的css样式编写是没有作用域的(属于全局的css),样式会渗透到子组件中去,样式之间会相互影响
  ```

- css-Modules

  ```js
  * .css/.less/.scss 等样式文件都需要修改成 .module.css/.module.less/.module.scss
  * 优点: 有自己的作用域,样式之间会相互影响
  * 缺点: 1.不能使用连接符(.home-title)，在JavaScript中是不识别的
         2.所有的className都必须使用{style.className} 的形式来编写
         3.不方便动态来修改某些样式，依然需要使用内联样式的方式
  ```

- css-in-js

  ```js
  * 要使用css-in-js需要有对应的库
  * 1.styled-components  2.emotion  3.glamorous
  * npm install styles-components - 高亮插件: vscode-styled-components
  * 优点: 1.支持子元素单独抽取到一个样式组件
  	    2.支持接受外部传入的props
          3.可以通过attrs给标签模板字符串中提供的属性
  		4.可以从一个单独的文件中引入变量
          5...
  ```

- classnames

  ```js
  * 是一个用于动态添加classname的一个库
  * npm install classnames
  ```

  





## 3. Redux

### 3.1 什么是redux？redux的核心思想是什么？核心的原则有哪些?

* Redux 是 JavaScript应用 的状态容器，提供可预测的状态管理

**redux核心思想**

- state: 
  - 管理状态的对象,其它的代码不能随意修改state,要想更新 state 中的数据,需要发起一个 action
- action
  - action 就是一个普通 JavaScript 对象 用来描述发生了什么
  - 强制使用 action 来描述所有变化带来的好处是可以清晰地知道应用中到底发生了什么
  - 最终，为了把 action 和 state 串起来，开发一些函数，这就是 reducer
- reducer
  - reducer 只是一个接收 state 和 action，并返回新的 state 的函数

**核心原则:**

- 单一数据源
  - Redux并没有强制让我们不能创建多个Store，但是那样做并不利于数据的维护
  - 单一的数据源可以让整个应用程序的state变得方便维护、追踪、修改
- state是只读的
  - 唯一修改State的方法一定是触发action
  - 这样可以保证所有的修改都被集中化处理，并且按照严格的顺序来执行
- 使用纯函数来执行修改
  - 通过reducer将 旧state和 actions联系在一起，并且返回一个新的State
  - 所有的reducer都应该是纯函数，不能产生任何的副作用



### 3.2 为什么需要redux?

JavaScript开发的应用程序，已经变得越来越复杂了：

* JavaScript需要管理的状态越来越多，越来越复杂
* 这些状态包括服务器返回的数据、缓存数据、用户操作产生的数据等等，也包括一些UI的状态，比如某些元素是否被选中，是否显示加载动效，当前分页

管理不断变化的state是非常困难的：

* 状态之间相互会存在依赖，一个状态的变化会引起另一个状态的变化，View页面也有可能会引起状态的变化
* 当应用程序复杂时，state在什么时候，因为什么原因而发生了变化，发生了怎么样的变化，会变得非常难以控制和追踪

React是在视图层帮助我们解决了DOM的渲染过程，但是State依然是留给我们自己来管理

* 无论是组件定义自己的state，还是组件之间的通信通过props进行传递；也包括通过Context进行数据之间的共享
* React主要负责帮助我们管理视图，state如何维护最终还是我们自己来决定

**Redux就是⼀个帮助我们管理State的容器，提供了可预测的状态管理**



## 4. React Router

### 4.1 什么是React Router?

* 





### 4.2 页面传递参数有几种方式?





