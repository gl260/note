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

* JSX 是J avaScript XML 的简写
* JSX是⼀种JavaScript的语法扩展
* 它用于描述我们的UI界面，并且可以和JavaScript融合在一起使用
* 它不同于Vue中的模块语法，我们不需要专门学习模板语法中的一些指令（比如v-for、v-if、v-else、v-bind）





### 1.4 JSX转换的本质是什么?

* jsx是通过babel工具转换编译成React代码的
* 本质
  - jsx 仅仅只是 React.createElement(component, props, ...children) 函数的语法糖
  - 所有的jsx最终都会被转换成React.createElement的函数调用





### 1.5 为什么React选择了JSX

* JSX 的是 Javascript 的语法糖
  * JSX 主要用于声明 React 元素，但 React 并不强制使用 JSX，即使用了 JSX 语法，最终在编译的过程中也会被 Babel 编译成 React.createElement, 所以JSX 更像 React.createElement 的语法糖
  * React 团队并不想引入 Javascript 之外的体系，而是希望通过合理的关注点分离来保持组件开发的纯粹性。
* 方案对比
  * 模版 -- React 团队认为模版不应该成为开发中的关注点，因为引入模版语法，模版指令等是一种不佳的方案
  * 模版字符串 -- 模版字符串的结构会造成多次的内部嵌套，使代码的结构变的复杂和更加的难以维护
  * 所以 React 最终选择的JSX，因为其跟 React的思想更加的贴合，不需要引入更多的概念





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

回答思路：**命名方式-->语法-->阻止浏览器默认行为-->优点-->执行顺序**

* **命名方式**：原生事件全为小写，react事件为小驼峰

* **事件函数处理语法**：原生为字符串，react为函数

  ```jsx
  // 原生HTML
    <button onclick="handleClick()">Click Me</button>
  // React
  	handleClick() {}
    render() {
      return <button onClick={this.handleClick}>Click Me</button>;
    }
  ```

* **阻止浏览器的默认行为**：react不能用return false来阻止，而必须调用event.preventDefault()来阻止。

* **相比HTML事件React事件的优点**：

  * 兼容所有浏览器，更好的跨平台
  * 将事件同意存放在一个事件池（数组），减少了内存消耗，避免频繁的增删
  * 便于react统一管理，提高了事件机制的执行效率

* **执行顺序**：原先先，合成事件后，需避免原生事件与合成事件混用，若原生事件[阻止冒泡](https://so.csdn.net/so/search?q=阻止冒泡&spm=1001.2101.3001.7020)会导致合成事件无法执行





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

* 函数式组件

```jsx
import React, { useRef, useEffect } from 'react';

const cpn = () => {
  const myRef = useRef(null); // 创建一个 ref
  useEffect(() => {
    console.log(myRef.current); // 输出对应的 DOM 元素
  }, []);
  return <div ref={myRef}>Hello, World!</div>; // 将 ref 赋给 DOM 元素
}

export default cpn
```





### 1.13 说说你对React context的理解

在React中，数据传递⼀般使用props传递数据，维持单向数据流，这样可以让组件之间的关系变得简单且可预测，但是单项数据流在某些场景中并不适用。单纯一对父子组件传递并无问题，但要是组件之间层层依赖深入，props就需要层层传递显然，这样做太繁琐了。

Context 提供了一种在组件之间共享此类值的方式，而不必显式地通过组件树的逐层传递 props

**简单说就是，当你不想在组件树中通过逐层传递props或者state的方式来传递数据时，可以使用Context来实现跨层级的组件数据传递。**

JS的代码块在执⾏期间，会创建⼀个相应的作⽤域链，这个作⽤域链记录着运⾏时JS代码块执⾏期间所能访问的活动对象，包括变量和函数，JS程序通过作⽤域链访问到代码块内部或者外部的变量和函数。

假如以JS的作用域链作为类比，React组件提供的Context对象其实就好比一个提供给子组件访问的作用域，而Context对象的属性可以看成作用域上的活动对象。由于组件 的 Context 由其父节点链上所有组件通 过getChildContext（）返回的Context对象组合而成，所以，组件通过Context是可以访问到其父组件链上所有节点组件提供的Context的属性。





### 1.14 类组件与函数组件有什么异同?

* 函数组件是通过js函数定义的组件, 接受props作为输入, 返回一个React元素. 函数组件通常用于无状态组件

  * 函数组件的特点是语法简洁 易于理解. 随着React Hooks的引入, 函数组件也可以管理状态和使用生命周期方法

* 类组件是通过ES6类定义的组件, 必须继承自React,compoment 类组件可以管理状态和使用生命周期方法

* 区别

  * 编写形式: 函数组件使用函数定义 类组件使用类定义
  * 状态管理: 函数组件使用useState和其他Hooks管理状态, 类组件使用this.state和this.setState
  * 生命周期: 函数组件使用useEffect模拟生命周期方法, 类组件直接使用生命周期方法

  ```js
  // 对应类组件中的componentDidMount生命周期
  useEffect(() => {
      console.log("Hello");
  }, []);
  // 如果在useEffect回调函数中return一个函数，则return函数会在组件卸载的时候执行，正如componentWillUnmount
  useEffect(() => {
      console.log("Hello");
    	return () => {
         console.log("Bye");
      };
  }, []);
  ```

  * 调用方式: 函数组件直接调用函数, 类组件需要实例化后调用render方法

  ```js
  // 如果是一个函数组件，调用则是执行函数即可：
  // 你的代码 
  function SayHi() { 
      return <p>Hello, React</p > 
  } 
  // React内部 
  const result = SayHi(props) // » <p>Hello, React</p >
  
  // 如果是一个类组件，则需要将组件进行实例化，然后调用实例对象的render方法：
  // 你的代码 
  class SayHi extends React.Component { 
      render() { 
          return <p>Hello, React</p > 
      } 
  } 
  // React内部 
  const instance = new SayHi(props) // » SayHi {} 
  const result = instance.render() // » <p>Hello, React</p >
  ```

* 选择

  * 函数组件语法更简洁, 适合简单的UI元素和无状态组件
  * 类组件适合需要复杂的状态管理和生命周期方法的组件
  * 随着Hooks的引入, **函数组件**的功能已经大大增强, **已成为React开大的首选**



### 1.15 React重要的组件生命周期有哪些？分别列出他们的作用。

**我们说的React生命周期,主要说的是类的生命周期, 因为函数式组件是没有生命周期函数的**

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



### 1.19 react中组件间通信的方法

* 父传子 props

* 子传父
  * 通过回调函数实现子组件向父组件传递数据
  * 实现方式
    * 父组件通过 `props` 传递一个回调函数给子组件。
    * 子组件调用该回调函数并传递数据

* 跨层级组件通信 Context API
  * 使用 React 的 `Context API` 在组件树中跨层级传递数据。
  * **实现方式**：
    - 使用 `React.createContext` 创建上下文。
    - 通过 `Provider` 提供数据，通过 `Consumer` 或 `useContext` 消费数据。

* 全局状态管理(**Redux、Zustand、Recoil 等**)
  * 对于复杂的应用，可以使用全局状态管理库来管理组件间的共享状态
* 事件总线(Event Bus)
  * 通过自定义事件系统实现任意组件间的通信
* Ref和ForwardRef
  * 通过 `ref` 直接访问子组件的实例或 DOM 元素。
  * **实现方式**：
    - 使用 `React.forwardRef` 将 `ref` 传递给子组件。
    - 父组件通过 `ref` 直接调用子组件的方法或访问其 DOM。

对于简单应用，`props` 和 `Context API` 通常足够；对于复杂应用，推荐使用 Redux、Zustand 等全局状态管理工具





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



### 3.3 redux的使用

基本使用

```shell
npm install @/reduxjs/toolkit react-redux
```

* 目录划分 (如果我们将所有的逻辑代码写到一起，那么当redux变得复杂时代码就难以维护)

  * actionCreators.js
  * constants.js
  * index.js
  * reducer.js

  ```js
  -store
  --modules
  ---功能名字
  ----actionCreators.js
  ----constants.js
  ----index.js
  ----reducer.js
  --index.js // 出口文件
  
  --index.js // 出口文件
  import { configureStore } from '@/reduxjs/toolkit';
  import mainReducer from './modules/main';
  import portReducer from './modules/port';
  
  const store = configureStore({
    reducer: {
      main: mainReducer,
      port: portReducer
    }
  });
  
  export default store;
  ```

  ```js
  // actionCreators.js --- 定义Action创建函数
  import * as actionTypes from "./constants";
  export const addCountAction = (add) => ({
    type: actionTypes.ADD_COUNT,
    add,
  });
  export const subCountAction = (sub) => ({
    type: actionTypes.SUB_COUNT,
    sub,
  });
  ```

  ```js
  // constants.js --- Action函数的type类型
  export const ADD_COUNT = "add_count";
  export const SUB_COUNT = "sub_count";
  ```

  ```js
  // index.js --- reducer出口
  import reducer from "./reducer";
  export default reducer
  ```

  ```js
  // reducer.js --- 创建一个 Reducer 来处理这些 Action
  import * as actionTypes from "./constants";
  const initialState = {
    counter: 100,
  }
  function reducer(state = initialState, action) {
    switch (action.type) {
      case actionTypes.ADD_COUNT:
        return { ...state, counter: state.counter + action.add };
      case actionTypes.SUB_COUNT:
        return { ...state, counter: state.counter - action.sub };
      default:
        return state;
    }
  }
  export default reducer;
  ```

* **这种目录划分代码依旧非常的混乱, redux的编写逻辑过于的繁琐和麻烦**

Redux Toolkit

* Redux Toolkit 是官方推荐的编写 Redux 逻辑的方法 (有点类似Vuex)
* 在很多地方为了称呼方便，也将之称为“RTK”

```shell
npm install @reduxjs/toolkit react-redux
```

* configureStore
  * 包装createStore以提供简化的配置选项和良好的默认值
* createSlice
  * 接受reducer函数的对象、切片名称和初始状态值，并自动生成切片reducer，并带有相应的actions
* createAsyncThunk
  * 接受一个动作类型字符串和一个返回承诺的函数，并生成一个pending/fulfilled/rejected基于该承诺分派动作类型的 thunk

```js
// modules/main.js
import { createSlice } from '@/reduxjs/toolkit';

const mainSlice = createSlice({
  name: 'main',
  initialState: {
    isHome: true,
    isMenuActive: '0'
  },
  reducers: {
    setIsHome(state, { payload }) {
      state.isHome = payload;
    },
    setIsMenuActive(state, { payload }) {
      state.isMenuActive = `${payload}`;
    }
  }
});

export const { setIsHome, setIsMenuActive } = mainSlice.actions;

// 定义了一个selectors selectMapTopBar 来替代 Vuex 中的 getters

export const selectMapTopBar = (state) => {
  const { sidebar } = state.app;
  return sidebar.map(({ children, ...other }) => other);
};

export default mainSlice.reducers;

/**
 * 使用selectMapTopBar
 *  import React from 'react';
    import { useSelector } from 'react-redux';
    import { selectMapTopBar } from '@/store';

    const Menus = () => {
      const topBarItems = useSelector(selectMapTopBar);

      return (
        <div className="top-bar">
          {topBarItems.map((item, index) => (
            <div key={index} className="top-bar-item">
              {item.name}
            </div>
          ))}
        </div>
      );
    };

  export default Menus;
 */
```

```js
// index.js
import { configureStore } from '@/reduxjs/toolkit';
import mainReducer from './modules/main';
const store = configureStore({
  reducer: {
    main: mainReducer,
  }
});

export default store;
```

* 使用

  * `useSelector` 是一个 React-Redux 提供的钩子，用于从 Redux Store 中提取状态（state）

  ```jsx
  import { useSelector } from 'react-redux';
  const Counter = () => {
    const count = useSelector(state => state.counter); // 提取 counter 状态
    return <div>{count}</div>;
  };
  ```

  * `useDispatch` 是一个 React-Redux 提供的钩子，用于获取 `dispatch` 函数

  ```jsx
  import { useDispatch } from 'react-redux';
  import { increment } from './actions';
  const Button = () => {
    const dispatch = useDispatch();
    return <button onClick={() => dispatch(increment())}>Increment</button>;
  };
  ```

  * `shallowEqual` 是一个 React-Redux 提供的工具函数，用于浅比较两个对象是否相等
    * 在 `useSelector` 中，用于优化性能，避免不必要的重新渲染。
    * 当 `useSelector` 返回的对象或数组发生变化时，`shallowEqual` 可以检查其属性或元素是否发生变化，而不是直接比较引用。

```jsx
import { setIsHome, setIsMenuActive } from '@/store/modules/main'
import { shallowEqual, useDispatch, useSelector } from 'react-redux'

const rr = memo(() => {
  const {roomList, isLoading} = useSelector((state) => {
    roomList: state.entire.roomList,
    isLoading: state.entire.isLoading
  },shallowEqual) // 使用 shallowEqual 避免不必要的重新渲染
  const dispatch = useDispatch()
  dispatch(setIsHome(传入的值))
})
export default rr
```









## 4. React Router

### 4.1 什么是React Router?

* 





### 4.2 页面传递参数有几种方式?





## 5.react项目创建流程

* create-react-app

  ```js
  create-react-app 项目名称(不能包含大写字母)
  ```

  * 这种方式创建的react项目默认是webpack打包
  * 需要安装craco(类似Vue外抛的vue.config.js), 在根目录下创建craco.config.js

  ```js
  npm install @craco/craco -D
  ```
  ```js
  // craco.config.js
  const path = require('path');
  
  module.exports = {
    // webpack
    webpack: {
      alias: {
        '@': path.resolve(__dirname, 'src')
      }
    }
  };
  ```

  

* vite

  ```js
  npm create vite@latest 项目名称
  ```

  * 按照提示选择“react”模板创建项目
  * 这种方式创建的就是vite打包的



## 6. react完全自动按需导入andt(待补充)

```js
npm install unplugin-auto-import -D

// vite.config.js
import AutoImport from 'unplugin-auto-import/vite';
export default defineConfig({
  plugins: [
    AutoImport({
      imports: [
        {
          antd: [
            'Button',
            'Input'
            // 添加其他你需要的组件
          ]
        }
      ],
      dts: true // 生成类型声明文件
    }),
  ]
});

// 页面不会报错 但是vscode会提示Button is not defined
```



































