##  1. Vue基础

### 1.0 说说你对Vue的理解?

Vue 是⼀套⽤于构建⽤户界⾯的渐进式 JavaScript框架

* 什么是渐进式框架? 怎么理解这个渐进式?

  我的理解就是 我们在使用vue时,可以只使用vue的某些部分或功能,而不需要立即的采用整个框架

  也就是说我们可以根据自己的需求和项目的特点 逐步应用框架的功能

  在vue中我们可以逐渐使用其模板语法 组件系统 状态管理 路由等不同的特性 不需要某些特性,我们也可以不使

  用,比如我们的项目比较简单 完全可以不使用vue提供的状态管理工具vuex

  这种方式可以让我们在使用vue时,更加的平滑 降低学习成本
  
  

基于标准 HTML、CSS 和 JavaScript 构建

并提供了一套声明式的、组件化的编程模型，帮助你高效地开发用户界面

**Vue核心特性**

* 数据驱动用的是MVVM
  * 但是官网也有说到 没有完全遵循MVVM模型 但是Vue的设计也受到了它的启发
* 组件化开发
  * Vue、React、Angular、包括小程序的开发,都是采用的组件化开发思想
  * 组件化开发就是将一个页面拆分成一个个小的功能块，每个功能块完成属于自己这部分独立的功能
  * **作用: **这样管理和维护页面就变得非常容易了
  * 组件化提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用
  * 任何的应用都会被抽象成一颗组件树
* 有自己的指令系统
  * 带有 v- 前缀的特殊属性作用
* 模板语法
  * vue中的template 语法是固定的，只有 v-if、v-for 等等语法，也就是说，template 遇见条件渲染就是要固定的选择用 v-if 相对于react中的jsx想实现条件渲染可以用 if else，也可以用三元表达式，还可以用任意合法的 JavaScript 语法
* 单位件组件  Single-File Components --> **SFC**
  * 我们可以使用一种类似 HTML 格式的文件来书写 Vue 组件，它被称为**单文件组件** 也被称为 `.vue` 文件
  * 顾名思义，Vue 的单文件组件会将一个组件的逻辑 (JavaScript)，模板 (HTML) 和样式 (CSS) 封装在同一个文件里
* 生命周期钩子
* 状态管理 Vuex
* 路由管理 Vue Router



### 1.1 什么是MVVM?

* MVC和MVVM都是⼀种软件的体系结构 MVC最先是后端出的 后面才出现了前端MVC MVVM
* MVC、MVP 和 MVVM 是三种常见的软件架构设计模式，主要通过分离关注点的方式来组织代码结构，优化开发效率
* MVVM是**Model-View-ViewModel**的简写
  * View: 视图 DOM-->负责将数据模型转化为UI展示出来
  * Model: 模型层 数据层-->Vue中的data数据
  * ViewModel: 视图模型层-->用来连接Model和View 简单来说就是Vue源码
* 官方有说到 - 虽然没有完全遵循 MVVM 模型，但是 Vue 的设计也受到了它的启发
* 结论: 将ui结构和业务逻辑分开，通过ViewModel在ui结构和业务逻辑之间进行通信
* 用MVVM开发页面的优势:
  * 低耦合：像html css js 基本不在一起写
  * 可重用性高
  * 双向数据绑定的模式，实现了View和Model的自动同步，因此开发者只需要专注对数据的维护操作即可，而不需要一直操作 dom。

##### 什么是MVC

* Model: 模型 --- 程序需要操作的数据或信息。
* View: 视图 --- 提供给用户的操作界面，是程序的外壳。
* Controller: 控制器 --- 它负责根据用户从"视图层"输入的指令，选取"数据层"中的数据，然后对其进行相应的操作，产生最终结果。



### 1.1 说说Vue双向绑定的原理

* Vue的双向绑定我们需要先理解MVVM

  * MVVM框架的的核心就是双向绑定, 其原理是通过**数据劫持+发布订阅模式**相结合的方式来是实现的
  * 简单来说就是数据层发生变化的时候，可同布更新视图层，当视图层发生变化的时候，同步更新数据层

* 当用户操作 View，ViewModel 感知到变化，然后通知 Model 发生相应改变；反之当 Model 发生改变，ViewModel也能感知到变化，使 View 作出相应更新

* 双向绑定的核心Object.defineProperty()

  ```js
  数据发⽣变化的时候，视图也就发⽣变化，当视图发⽣变化的时候，数据也会跟着同步变化
  其原理是通过数据劫持和发布订阅模式实现的
  首先，Vue通过Object.defineProperty()方法对数据进行劫持，监听数据的变化，并通过getter和setter方法对数据进行读写
  其次，Vue通过发布订阅模式，维护了一个订阅者数组，当数据发生变化时，Vue会通知所有订阅者进行更新。因此，当用户在页面上进行修改时，Vue会更新对应的数据，并通知所有订阅者更新视图，同时当数据发生变化时，Vue也会更新对应的视图，通过这样的机制，Vue实现了双向数据绑定，使得数据和视图的变化可以互相影响
  
  补充：订阅者是Vue中的一个概念，它是一个用于管理更新视图的对象，当数据发生变化时，Vue会通知所有的订阅者进行更新，在Vue中，每一个挂载到视图上的组件，或者每一个watcher，都可以被看成一个订阅者，他们订阅了某一个数据的变化，并等待数据发生变化时进行更新，订阅者是Vue实现双向数据绑定的关键组成部分，管理着数据和视图之间的关系，保证了数据的变化能够及时反应到视图上
  ```



### 1.2 说说你对SPA单页面的理解 它们的优缺点是什么?

* SPA（ single-page application ）单页面应用
* 页面在初始化时加载相应的 HTML、JavaScript 和 CSS
* ⼀旦⻚⾯加载完成，SPA 不会因为⽤户的操作⽽进⾏⻚⾯的刷新或跳转
* 取⽽代之的是利⽤路由机制实现 HTML 内容的变换，避免⻚⾯的重新加载
* 优点
  * 对用户的体验友好,内的改变不引起页面的刷新
  * SPA对服务器压力小
  * 前后端职责清晰,前端进⾏交互逻辑，后端负责数据处理
* 缺点
  * 首次加载耗时多: 所以按需加载就显得尤为重要
  * SEO 难度较⼤：由于所有的内容都在⼀个⻚⾯中动态替换显示，所以在 SEO 上其有着天然的弱势。



### 1.3 v-show 与 v-if 有什么区别?

* 在用法上
  * v-show不支持template
  * v-show不能和v-else一起使用
* 本质区别
  * v-show无论是否是在浏览器上显示,它的DOM都是真实存在的,只是通过display属性切换
  * v-if 条件为false时,就压根不会渲染DOM
* 开发中怎样选择?
  * 需要频繁的显示和隐藏 使用v-show
  * 不会频繁 就使用v-if



### 1.4 数组中有哪些方法会触发视图的更新?

* Vue 能够侦听响应式数组的变更方法，并在它们被调用时触发相关的更新。这些变更方法包括：
* 会修改原来数组的方法,就会触发视图更新 (7种)
  * shift() --- 移除数组的第一项
  * pop() --- 删除数组的最后一位
  * push()
  * unshift() ---（在开头)向数组添加一个元素
  * splice() ----截取数组
  * sort() ----排序数组
  * reverse() ----反转数组
* 像filter()、concat() 和 slice() 会⽣成新的数组,所以不会触发视图更新



### 1.5 Vue中 v-for的key有什么所用?

* 在使用v-for进行列表渲染时,通常会给元素绑定一个key属性
* 这个key有什么作用呢?
  * 用在虚拟DOM算法上
  * key属性主要是为了**更高效的更新虚拟DOM**，用于dom diff算法，在比较新旧节点列表(识别哪些节点是新的、哪些是已存在的)
    * vue使用的虚拟dom，不直接操作dom元素，在操作虚拟dom的时候又使用了diff算法。diff算法的实现基于两个假设： 两个相同的组件产生类似的DOM结构，不同的组件产生不同的DOM结构。
  * 没有 key 时，Vue 会默认使用“就地更新”策略，可能导致不正确的更新
  * 有key时，如果列表顺序变化，Vue 能够基于 `key` 重新排序元素而不是重新渲染。
* key 的主要作用是帮助 Vue 识别节点变化，减少不必要的 DOM 操作

##### 为什么key不要用index

* 若用数组索引 index 做为key
* 当向数组中指定位置插入一个新元素后，因为这时候会重新更新index索引
* 对应着后面的虚拟DOM的key值全部更新了
* 这个时候还是会做不必要的更新，就像没有加key一样
* 但如果是静态数据，用索引号index做key值是没有问题的



### 1.6 computed和method有什么区别?

* 都可以通过this来访问 
* 都可以对⼀些数据进⾏处理和计算
* 对于任何包含响应式数据的复杂逻辑，你都应该使用计算属性
  * 响应式数据: 在data里面的都是响应式数据
* 区别
  - 计算属性是有缓存的
  - 计算属性会基于它们的依赖关系进行缓存
  - 在数据不发生变化时，计算属性是不需要重新计算的
  - 但是如果依赖的数据发生变化，在使用时，计算属性依然会重新进行计算



### 1.7 什么是双向绑定? v-model的本质是什么?

* 首先我们的Vue是双向绑定的框架，双向绑定由三个重要部分构成MVVM

* 数据发⽣变化的时候，视图也就发⽣变化，当视图发⽣变化的时候，数据也会跟着同步变化

* 表单v-model的本质: 背后有两个操作

  * v-bind绑定value属性的值
  * v-on绑定input事件监听到函数，函数会获取最新的值赋值到绑定的属性中
  * 可以减少大量繁琐的事件处理代码 提高开发效率

  ```html
  <input type="text" :value="message" @input="inputChange" />
  ```

* 组件v-model的本质

  * 将内部原生 `input` 元素的 `value` attribute 绑定到 `modelValue` prop
  * 输入新的值时在 `input` 元素上触发 `update:modelValue` 事件

  ```vue
  <counter :modelValue="message" @update:modelValue="message= $event"></counter>
  
  //父组件
  <counter v-model="message"></counter>
  data(){
      return{
          message: 10,
      }
  }
  
  //子组件
  <h2>counter: {{ modelValue }}</h2>
  <button @click="changeCounter">修改counter</button>
  props: {
      modelValue: {
        type: Number,
        default: 0,
      },
      },
      emits: ["update:modelValue"],
      methods: {
      changeCounter() {
        this.$emit("update:modelValue", 999);
      },
  },
  ```

  

### 1.8 data选项为什么是一个函数而不是一个对象?

* JS中对象是引用类型的数据, 当多个实例引用同一个对象时, 只要对一个实例进行操作, 其它实例都会变化
* ⽽在Vue中，我们更多的是想要复⽤组件，那就需要每个组件都有自己的数据，这样组件之间才不会相互干
* 所以组件的数据就不能是对象的形式, 而是要以函数的形式
* 数据以函数返回值的形式定义
* 这样当我们每次复⽤组件的时候，就会返回⼀个新的data，也就是说每个组件都有自己的私有数据空 间，它们各自维护自己的数据，不会干扰其他组件的正常运行
* `vue`实例的时候定义`data`属性既可以是一个对象，也可以是一个函数
* 组件中定义`data`属性，只能是一个函数
* 结论
  * 根实例对象`data`可以是对象也可以是函数（根实例是单例），不会产生数据污染情况
  * 组件实例对象`data`必须为函数，目的是为了防止多个组件实例对象之间共用一个`data`，产生数据污染



### 1.9 Vue data 中某一个属性的值发生改变后，视图会立即同步执行重新渲染吗？

* 不会立即同步执行重新渲染
* Vue 实现响应式并不是数据发生变化之后 DOM 立即变化，而是按⼀定的策略进行 DOM 的更新

**Vue 在更新 DOM 时是异步执行的。**只要侦听到数据变化， Vue 将开启⼀个"任务队列"，并缓冲在同⼀事件循环中发⽣的所有数据变更

异步更新是：Vue会在本轮数据更新后，再去异步更新视图!

* 为什么不是同步更新?
  * 首先要明确一点：vue是组件级更新,也就是说，每一次的更新都是渲染整个组件
  * 如果是同步的话，一旦修改了`data`属性，就会更新视图，很耗性能，用户体验感也不好



### 1.10 sass是什么?如何在Vue中安装和使用?

* sass是⼀种CSS预处理器语⾔，除此之外，less、stylus也是常⻅的CSS预处理器语⾔
* sass安装和使⽤
  * ⽤npm安装加载程序（ sass-loader、 css-loader等加载程序)
  * 在webpack.confifig.js中配置sass加载程序



### 1.11 在Vue开发环境中调用API接口, 如何避免跨域?

* 在vue.config.js中的devServer选项中的proxy中配置反向代理
* 在vite.config.js中的server选项中的proxy中配置反向代理
* 直接后端开发⼈员配置cors



### 1.12 v-if和-for一起使用的弊端及解决办法

* 2.x 版本中在⼀个元素上同时使⽤ v-if 和 v-for 时， v-for 会优先作⽤

* 3.x 版本中 v-if 总是优先于 v-for ⽣效

* 解决方法:

  * 一般要避免在同⼀元素上同时使⽤两者
  * 可以在外层嵌套template（页面渲染不生成dom节点）

  ```vue
  <template v-if="isShow">
      <p v-for="item in items">
  </template>
  ```

  * 如果条件出现在循环内部，可通过计算属性`computed`提前过滤掉那些不需要显示的项



### 1.13 谈谈你对keep-alive的理解

* keep-alive 是 Vue 内置的⼀个组件，它的功能是在多个组件间动态切换时缓存被移除的组件实例
  * 用来缓存组件的, 从一个组件切换到另一个组件时, 这个组件不会被销毁, 而是被缓存起来
* ⼀般结合路由和动态组件⼀起使⽤，⽤于缓存组件
* 提供 include 和 exclude 属性，都⽀持字符串或正则表达式
* 对应两个生命周期钩⼦函数 activated 和 deactivated
  * activated: 当组件被激活时触发
  * deactivated: 当组件被移除时触发



### 1.14 说说插槽的作用和平时开发中的应用

* 插槽的作用
  * 可以理解成一个站位的
  * ⽀持在⽗组件⾃定义⼦组件中的个内容
  * 让⼦组件更具有通⽤性
* 应⽤
  * 在封装组件时，组件中的某个内容是动态的或不确定的，就可以使⽤插槽
  * 在使⽤第三⽅库时，往往会通过使⽤插槽类⾃定义第三⽅组件中的某些内容



### 1.15 computed和watch的区别

* computed特点: 具有响应式的返回值

  * 最常见的使用方式是设置一个函数,返回计算之后的结果
  * 计算属性是具备缓存性的,只有依赖的数据发生改变的时候，才会重新进行计算，否则会直接从缓存中读取
  * 计算属性它不支持异步，当computed内有异步操作时是无效的，无法监听到数据的变化
  * 计算属性的常用场景是简化行内模板中的表达式

  ```js
  const count = ref(1)
  const One = computed(() => count.value + 1)
  ```

* watch特点: 侦听变化, 执行回调

  * watch没有返回值但是可以执行异步操作
  * computed也是可以传递对象的 watch可以传递对象,设置deep,immediate选项
  * 侦听器的常用场景是状态变化后做一些额外的DOM操作或者异步操作




### 1.16 Vue中有哪些常用的修饰符

* 事件修饰符: stop once prevent sync

* 表单修饰符: lazy trim number

* stop

  * 阻止了事件冒泡，相当于调用了`event.stopPropagation`方法

  ```markdown
  <div @click="shout(2)">
      <button @click.stop="shout(1)">ok</button> 
  </div> 
  ```

* once

  * 绑定了事件以后只能触发一次，第二次就不会触发

  ```markdown
  <button @click.once="shout(1)">ok</button>
  ```

* prevent

  * 阻止默认事件，相当于调用了`event.preventDefault`方法

  ```markdown
  <form @submit.prevent="onSubmit"></form>
  ```

* sync

  * 对prop进行双向绑定

* lazy

  * 输入框改变，这个数据就会改变，lazy这个修饰符会在光标离开input框才会更新数据

  ```markdown
  <input type="text" v-model.lazy="value">
  ```

* trim

  * 输入框过滤首尾的空格

  ```markdown
  <input type="text" v-model.trim="value">
  ```

* number

  * v-model绑定后的值总是string类型 希望将内容转换成数字,使用.number修饰符



### 1.17 Vue中过滤器的使用(vue2)

* **从 Vue 3.0 开始，过滤器已删除，不再支持**
  
* 官方建议：用方法调用或计算属性替换过滤器。
  
* vue中允许自定义过滤器，用来对文本进行格式化处理

* 过滤器可以用在两个地方：双花括号插值语法 和 v-bind表达式

* 可以注册局部过滤器(在组件中注册)，也可以在创建 Vue 实例之前全局定义过滤器

  * 局部

    ```js
    // 和message同级
    filter: {
       add: function(num) {
           return num > 10 ? "000" + num : num
       } 
    }
    ```

  * 全局

    ```js
    Vue.filter("add", function(num) {
        return num > 10 ? "0" + num : num
    })
    
    使用
    <div>{{ 33 | add }}</div>
    ```

* 过滤器参数

  ```js
  <div>{{ message | add(arg1, arg2) }}</div>
  
  filter: {
     add: function(value, arg1, arg2) {
         clg(value, arg1, arg2)
         return value + arg1 + arg2
     } 
  }
  ```

  



## 2. Component组件

### 2.1 父子组件的生命周期顺序

* 加载渲染过程： 
  * 父：beforeCreate，created，beforeMount
  * 子：beforeCreate，created，beforeMount，mounted
  * 父：mounted
* ⼦组件更新过程：⽗beforeUpdate -> ⼦beforeUpdate -> ⼦updated -> ⽗updated
* ⽗组件更新过程：⽗beforeUpdate -> ⽗updated 
* 销毁过程：⽗beforeDestroy -> ⼦beforeDestroy -> ⼦destroyed -> ⽗destroyed

##### 补充: Vue进入组件会默认执行那些生命周期

* beforeCreate，created，beforeMount，mounted

##### 补充: 在created中如何获取DOM?

* 只要将获取DOM的代码在异步中获取的就可以了
* 解释:
  * 因为像beforeCreate，created，beforeMount这些都是同步代码
  * 我们的js机制是要先执行完同步代码,才会执行异步代码
  * 所以无论在beforeCreate，created生命周期中获取DOM,只要将获取DOM的代码在异步中就好了
  * 比如：可以写在请求(axios)，setTimeout，nextTick(this.$nextTick),Promise.then等等

##### 补充: 为什么发送请求不在beforeCreate中?

* 因为: 如果请求是在methods中封装好了的,在beforeCreate调用的时候,beforeCreate阶段是拿不到methods里面的方法的(会报错)



##### 补充:  beforeCreate和created有什么区别?

* beforeCreate：没有$el 也没有$data 获取不到methods的方法
* created：有$data 可以获取methods的方法

```js
$el: this.$el --> 获取template下的根元素 (该组件实例管理的 DOM 根节点)

$data: this.$data() --> 获取data中的数据
```



##### 补充: 发送请求是在created还是mounted?

* 其实并不是说网络请求只能放在created中的
* 这个问题是需要看项目具体的业务需求
* 当组件之间有父子关系时,需要考虑父子组件之间生命周期的执行顺序的
* 如果当前组件没有依赖关系,那么放在哪个生命周期都是可以的



##### 补充: this在哪些生命周期中可以被访问到?

* 好像除了beforeCreate都是可以访问到的
* destroy -- 完全销毁一个实例 并不能清除DOM，仅仅销毁实例
* destroy 到底可不可以访问this? -- 测试了可以通过this去访问data中的数据



##### 补充: 使用keep-alive会执行哪些生命周期?

* 使用了keep-alive组件后,当前组件会额外的增加两个生命周期 (8+2)

```js
activated
deactivated
```

* 当前组件加入了keep-alive第一次进入组件时会执行5个生命周期

```js
beforeCreate，created，beforeMount，mounted，activated
```

* 当前组件加入了keep-alive第二次后就只会执行一个生命周期了

```js
activated
```



##### 补充: 你在什么情况下用过哪些生命周期?说说生命周期的使用场景

* 生命周期是要根据业务的情况和场景来选择的

```js
常用的有
created
mounted
activated
destroyed
```

* 如果我们需要同步下 获取DOM 这是需要在mounted中获取
* 网络请求的情况 -- 其实并不是说网络请求只能放在created中的
  * 这个问题是需要看项目具体的业务需求
  * 当组件之间有父子关系时,需要考虑父子组件之间生命周期的执行顺序的
  * 如果当前组件没有依赖关系,那么放在哪个生命周期都是可以的
* 设计到使用keep-alive -- activated
* beforeDestroy / destroyed -- 用于一些定时器或者一些事件的取消

![vue2生命周期](E:\Typora-文件\Typora图片位置\vue2生命周期.png)







### 2.2 组件通讯(传值)式有哪些?

* 父传子 / 子传父

  * 父传子

  ```js
  1.父组件引入子组件,绑定数据
  	<List :str1="str1"></List>
     子组件通过props来接收
     props: {
         str1: {
             type: String,
             default: ""
         }
     }
  2.子组件直接使用父组件的数据
  子组件通过this.$parent.str1使用父组件的数据
  这种方式可以直接修改父组件的数据,但是这样不符合Vue中的单项数据流
  ```

  * 子传父

  ```js
  1.在子组件中自定义事件 this.$emit
  2.父组件直接拿到子组件的数据
  通过ref来拿到组件的实例 --> 这种方式一般写在mounted生命周期中
  <List ref="child"></List>
  this.$refs.child
  ```

* Provide/Inject

* 组件实例: 通过ref来拿到组件的实例，调⽤实例的属性或⽅法进⾏传值

* 事件总线

* Vuex/Pinia



### 2.3 什么生命周期函数？Vue组件的生命周期函数有哪些？

* 每个Vue组件实例被创建后都会经过一系列初始化步骤，总共可以分为8个阶段

  * **创建前后, 挂载前后, 更新前后, 销毁前后**
  * 

* ⽣命周期函数

  * ⽣命周期函数是⼀些钩⼦函数（回调函数），在某个时间会被Vue源码内部进⾏回调
  * 通过对⽣命周期函数的回调，我们可以知道⽬前组件正在经历什么阶段

* Vue2的生命周期函数

  ```js
  // 组件的渲染过程: template -> ast -> render -> vDom -> 真实DOM -> 页面展示
  //组件从创建到销毁所调用的生命周期函数
  
  beforeCreate：创建组件实例之前，未初始化和响应式数据
  created：已初始化和响应式数据，可访问数据
  beforeMount：render调用，虚拟DOM生成，未转真实DOM
  mounted：真实DOM挂载完成
  
  beforeCreate
  1.创建组件实例
  created - (重要:1.发送网络请求 2.事件监听 3.this.$watch() 4.事件总线)
  
  2.template模板编译 将元素转成VNode
  
  beforeMount
  3.挂载到vDOM 根据vDOM -> 真实DOM -> 显示界面
  mounted - (重要: 元素已经被挂载,获取DOM,使用DOM)
  
  beforeUpdate
  4.数据跟新: 根据最新数据生成新的VNode,生成新的vDOM -> 真实DOM
  updated
  
  beforeUnmount
  5.组件移除挂载(不是销毁): 将之前挂载在vDOM中的VNode,从vDOM中移除,一旦一移除,在进行两个diff算法时,就会发现VNode就不存在了,就会将真实DOM做一个更新
  unmounted - (重要: 回收操作(取消事件监听))
  
  6.将组件实例销毁掉(是在unmounted之后的)
  ```

* Vue3的声明生命周期函数

  * beforeCreate -> 使用 setup()
  * created -> 使用 setup()
  * beforeMount -> onBeforeMount
  * mounted -> onMounted
  * beforeUpdate -> onBeforeUpdate
  * updated -> onUpdated
  * beforeDestroy -> onBeforeUnmount
  * destroyed -> onUnmounted

* 因为 setup 是围绕 beforeCreate 和 created 生命周期钩子运行的，所以不需要显式地定义它们

* 换句话说，这两个钩子中编写的任何代码都应该直接在 setup 函数中编写

* 在setup中,需要先注册生命周期函数才可以使用

  ```js
  import { 
  	onBeforeMount, 
      onMounted, 
      onBeforeUpdate, 
      onUpdated, 
      onBeforeUnmount, 
      onUnmounted
  } from "vue";
  ```
  
* setup和created谁先执行？

  * setup中没有beforeCreated和created钩子。因为setup的时候组件实例已经被创建了。vue会先执行setup的内容再执行optoins API



## 3. Composition API

### 3.1 什么是Composition API 和 Options API？区别?

* **Composition API（组合式 API）**
  * 组合式 API (Composition API) 是一系列 API 的集合，它是一个概括性的术语，涵盖了以下方面的 API：
    - 响应式 API：例如 `ref()` 和 `reactive()`
    - 生命周期钩子：例如 `onMounted()` 和 `onUnmounted()`
    - 依赖注入：例如 `provide()` 和 `inject()`
  * 组合式 API 是 Vue 3 及 Vue 2.7的内置功能
* **Options API（选项式 API）**
  * 在对应的属性中编写对应的功能模块, 比如data定义数据、methods中定义方法、computed中定 义计算属性、watch中监听属性改变......
  * 这样的代码过于分散,当组件变得更大时,**逻辑关注点**列表也会增长,对于一些没有编写过这些组件来说,会非常难以理解

* **组合式 API**: 就是将同一个**逻辑关注点**的相关代码收集在一起

* 区别
  * 在逻辑组织和逻辑复用方面，Composition API是优于Options API
  * Composition API乎是函数，会有更好的类型推断，对于TS的支持更友好
  * Composition API对 tree-shaking 友好，代码也更容易压缩
  * Composition API中见不到this的使⽤，减少了this指向不明的情况
    * 我们在使用 Composition API 的功能时，ref、computed 等功能都是从 Vue 中单独引入，而不是依赖 this 上下文，减少了this指向不明的情况
  * Composition API⽤起来稍微复杂⼀点，⽽Options API就非常简单、易于使用

###### Tree shaking是什么?

* 摇树(把多余的代码摇下来) 是一种通过清除多余代码方式来优化项目打包体积的技术
* 简单来讲，就是在保持代码运行结果不变的前提下，去除无用的代码
  * 在`Vue2`中，无论我们使用什么功能，它们最终都会出现在生产代码中。
  * 而`Vue3`源码引入`tree shaking`特性，将全局 API 进行分块。如果不使用其某些功能，它们将不会包含在基础包中



### 3.2 说说Vue3中setup函数的作用？

* 在Vue3中， setup() 函数充当了组件编写Composition API 的⼊⼝
* setup有两个参数
  * 第一个参数: 组件的 `props` , ⽗组件传递过来的属性会被放到props对象中
  * 第二个参数: 是一个setup上下文对象`context`
    * attrs: 所有的非prop的attribute
    * slots: 插槽
    * emit: 组件内部需要发出事件 emit（因为我们不能访问this，所以不可以通过 this.$emit发出事件）
    * expose: 暴露公共属性
* 可以在setup中可以定义响应式数据、方法、计算属性、侦听器等等
* 可以通过setup的返回值来替代data选项，让数据可以直接在template中使⽤



### 3.3 ref和reactive有什么区别？开发中如何选择？

* ref和reactive都是响应式的API，都可以⽤来定义响应式的数据
* ref可以包裹任意数据类型，reactive只能包裹复杂数据类型，⽐如对象、数组
* ref返回⼀个ref对象，在script中取值需要通过value属性，但是在模板中使⽤会进⾏解包不需要调⽤value
* reactive包裹的是复杂数据类型，直接取⾥⾯的属性即可
* ref⼏乎可以应⽤在任何场景，⽽且包含reactive适合的场景
* 开发中尽量选择ref



### 3.4 Composition API常见的几个函数与用法？

* ref: 包裹任意类型的值，将包裹的值加⼊响应式
* reactive: 包裹复杂类型的值，将包裹的值加⼊响应式
* compoted: computed会自动收集相关依赖，当依赖发生变化时，会自动进行更新
* 生命周期
  * Vue3中想要在beforeCreate和created中做的事，直接在setup中做即可

* watch
  * watch可以监听单个数据源，也可以监听多个数据源
  * watch是懒执⾏，第⼀次是不会执⾏的，immediate属性为 true
  * watch只有等到监听的数据源发⽣了变化后，才会执⾏第⼆个参数（回调） 
  * watch可以获取监听数据源的前后变化的值 
  * 侦听多个数据源的时候，第⼀个参数是数组类型
* watchEffect
  * watchEffect会自动收集依赖，立即运行一个函数
  * 同时响应式地追踪其依赖，并在依赖更改时重新执行
* toRefs
  * 对reactive进⾏解构后就失去了响应式的效果，因为reactive返回的是⼀个Proxy对象
  * 如果想要对reactive进⾏解构，需要对其包裹⼀个toRefs 
  * 这么做相当于为reactive中的每⼀个值包裹了⼀个ref



### 3.5  Vue3中的watch和watchEffect有什么区别？

* 都是用来侦听响应式数据的变化
  * `watchEffect`在使用时，传入的函数会立刻执行一次。
  * `watch`默认情况下并不会执行回调函数，除非我们手动设置`immediate`选项。
  * 如果我们不关心响应式数据变化前后的值，只是想拿这些数据做些事情，那么`watchEffect`就是我们需要的。
  * watch更底层，可以接收多种数据源，包括用于依赖收集的getter函数，因此它完全可以实现watchEffect的功能，同时由于可以指定getter函数，依赖可以控制的更精确，还能获取数据变化前后的值，因此如果需要这些时我们会使用watch
* watch --> 3.4
  * 侦听一个或多个响应式数据源，并在数据源变化时调用所给的回调函数
* watchEffect --> 3.4
  * 立即运行一个函数，同时追踪它的依赖，当这些依赖改变时重新执行该函数



### 3.6 说说Vue3中script setup语法糖的常见用法?

* `<script setup>` 是在单文件组件 (SFC) 中使用组合式 API 的编译时语法糖
  * 更少的样板内容，更简洁的代码
  * 能够使用纯 Typescript 声明 prop 和抛出事件
  * 更好的运行时性能
  * 更好的代码提示
* **defineProps**
  * 必须使⽤ defineProps API来声明props
* **defineEmits**
  * 必须使⽤ defineEmits API来声明 emits

* **defineExpose**
  * 可以通过 defineExpose 来指定组件中要暴露出去的属性
  * 都是可以直接使用的,不需要import引入



## 4. Vue Router路由

### 4.1 vue-router的两种模式

* **默认使用的是hash模式** 区别只在url的形式

  * hash模式，带#。如：http://localhost:8080/#/page，改变hash浏览器本身不会有任何请求服务器动作
  * history模式，不带#， 如：http://localhost:8080/page，基于HTML5的pushState、replaceState实现

  

  | **hash**                                                     | **history**                                                  |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | 有 # 号                                                      | 没有 # 号                                                    |
  | 能够兼容到IE8                                                | 只能兼容到IE10                                               |
  | 实际的url之前使⽤哈希字符，这部分url不会发送到服务器，不需要在服务器层⾯上进⾏任何处理 | 每访问⼀个⻚⾯都需要服务器进⾏路由匹配⽣成html⽂件再发送响应给浏览器，消耗服务器⼤量资源 |
  | 刷新不会存在 404 问题                                        | 浏览器直接访问嵌套路由时，会报 404 问题。需要后台配置支持。如果后台没有正确配置，访问时会返回 404 |
  | 不需要服务器任何配置                                         | 需要在服务器配置⼀个回调路由                                 |

* hash模式 这种方式使用和部署都比较简单

* history模式 url看起来更美观,但是在部署时需要做特殊的配置,web服务器需要做回退处理,否则会出现刷新页面404问题 --- 刷新页面可能会导致页面404,前端url必须与发送到服务器请求的url相同

* 注意 --- vue-router其实有三种模式

  * hash 和 history 是 SPA 单页应用程序的基础。也就是在浏览器环境中有着两种模式
  * abstract模式  当不在浏览器环境，比如 node 中时，就使用这种模式



### 4.2 什么是前端路由？前端路由的发展历程是怎么样的？

###### 前端路由发展历程

- **后端路由阶段**

  - 早期的网站开发,浏览器拿到的资源是已经被服务器渲染完成的,浏览器直接展示就可以
  - 不需要下载对应的html,css,js等

  ```js
  // 一个页面有自己对应的网址, 也就是URL
  // URL会发送到服务器, 服务器会通过正则对该URL进行匹配, 并且最后交给一个Controller进行处理
  // Controller进行各种处理, 最终生成HTML或者数据, 返回给前端
  ```

  - 后端路由就是由**服务器来维护** URL与HTML页面的映射关系
  - **优点:** 不需要单独加载任何的js和css(因为是服务器渲染好的), 可以直接交给浏览器展示, 这样也有利于SEO的优化
  - **缺点:** HTML代码和数据以及对应的逻辑会混在一起, 难以编写和维护

- **前后端分离**

  - 依然是后端渲染的模式(依然是后端来维护URL与HTML页面的映射关系)
  - Ajax的出现, 有了前后端分离的开发模式
  - 后端只提供API来返回数据，前端通过Ajax获取数据，并且可以通过JavaScript将数据渲染到页面中
  - **优点:** 前后端责任的清晰，后端专注于数据上，前端专注于交互和可视化上
  - 但是目前比较少的网站采用这种模式开发

- **单页面富应用阶段(前端路由)**

  - SPA: single page web application
  - SPA的特点就是在前后端分离的基础上加上一层前端路由
  - 前端维护着一个映射关系: URL与组件的映射关系
  - **前端路由的核心: **改变URL，但是页面不进行整体的刷新



### 4.3 路由跳转时如何传递数据？

* 动态路由
  * path: `/user/:id`
  * 获取动态路由的值的⽅式
    * 在template中：直接通过$route.params获取值
    * 在created中：通过 this.$route.params获取值
    * 在setup中：要使用 vue-router库给我们提供的一个hook -- useRoute
  
  ```js
  使用$router.push 拼接参数传参
  this.$router.push('/edit?name=add')
  
  使用name来确定匹配的路由，通过params来传递参数
  this.$router.push({
      name: 'login',
      params: {
          name: "add"
      }
  })
  
  接收参数 注意:route没有r
  this.$route.params.name
  ```
  
  
  
* query[ˈkwɪəri]
  * 在template中用$route.query获取到
  * 在created中，通过 this.$route.query获取值 
  * 在setup，使⽤ vue-router库提供的⼀个hook useRoute 来获取
  
  ```js
  router.push({
      path: "/about",
      query: {
        name: "大大怪将军",
        age: 18,
      },
    });
  
  接收参数 注意:route没有r
  this.$route.query.name
  ```
  
  



### 4.4 useRoute 和 useRouter的区别?

* **useRoute**: 返回当前路由地址 相当于在模板中使用 $route   ---   route: 路线            

  - 用在获取路由路径

  ```js
  import { useRoute } from "vue-router";
  const route = useRoute();
  const user1 = route.params.id;
  ```

* **useRouter**: 返回 router 实例   --- router: 路由器

  * 用在编程式导航上

  ```html
  不用router-link可不可以导航呢: 这种叫编程式导航
  <span @click="spanClick">首页</span>
  <button @click="buttonClick">关于</button>
  
  <router-view></router-view>
  ```

  ```js
  import { useRouter } from "vue-router";
  
  const router = useRouter();
  const spanClick = () => {
    router.push("/home");
  };
  
  const buttonClick = () => {
    router.push({
      path: "/about",
      query: {
        name: "大大怪将军",
        age: 18,
      },
    });
  };
  ```

##### 补充: router和route的区别?

route是当前路由 存储着当前路由的信息, 比如path query

router返回 router 实例,是一个全局路由,可以用来操作路由,项目中常用的就是拿来做路由跳转了



### 4.5 什么是路由(导航)守卫？路由守卫有什么作用？

* 路由守卫
  * vue-router 提供的导航守卫主要用来通过跳转或取消的方式守卫导航。
* 作用
  * 可以在进入路由之前进行某些判断，比如，检查token是否存在来判断用户是否已经登录。
  * 可以在路由守卫中进行页面的权限判断，比如，判断某个用户是否拥有该页面的权限。
  * 也可以用来记录页面的某些信息，比如，记录页面的滚动信息。



### 4.6 什么是vue-router动态路由

* 很多时候 我们在访问一个页面的时候 **一组页面** 都要同一个组件来映射 这个时候就要定义动态路由
* 比如说显示一个用户 `:id` id指明是哪一个用户
* 比如显示一个详情页 `:id` 商品的id
* path: `/user/:id`
* 获取动态路由的值的⽅式
  - 在template中：直接通过$route.params获取值
  - 在created中：通过 this.$route.params获取值
  - 在setup中：要使用 vue-router库给我们提供的一个hook -- useRoute



### 4.7 什么场景使用嵌套路由

当我们的页面足够复杂的时候使用



### 4.8 怎么实现路由懒加载呢？

* 当我们打包构建应用时，包会变得非常大，影响页面加载。利用路由懒加载我们能把不同路由对应的组件分割成不同的代码块，被访问到的时候才加载对应组件，使得更加高效，是一种优化手段
* 一般来说，我们应该对所有的路由**都使用动态导入**，是一个非常不错的选择
* 给`component`选项配置一个 **返回 Promise 组件的函数** 就可以定义懒加载路由
* 



## 5. Vuex和Pinia状态管理

### 5.1 说说你对Vuex的理解

* Vuex 是专门为 Vue.js 设计的**状态管理库**

* 什么是状态管理

  * 在开发中，应用程序需要处理各种各样的数据，这些数据需要保存在我们应用程序中的某一个位置，对于这些数据的管理我们就称之为是 **状态管理**

* 在Vue组件内部的数据是以**单项数据流**的形式来管理数据的

  * 单项数据流理解：我们的组件A可以使用state中的数据，但是不能改state中的数据
  * 状态 --> 视图 --> 操作 -------->状态 --> ... 	(只能从一个方向来修改状态)
  * **状态**，驱动应用的数据源；
  * **视图**，以声明方式将**状态**映射到视图；
* **操作**，响应在**视图**上的用户输入导致的状态变化。
  
  ![Snipaste_2022-10-11_12-27-00](E:\Typora-文件\Typora图片位置\Snipaste_2022-10-11_12-27-00.png)

##### Vuex的必要性

* 当我们遇到多个组件共享状态时，组件A 组件B都有一个相同的状态 那如果我们没有一个管理状态的地方，则这两个组件之间会发生状态的不同步，A改变了，B却不知道，还是按照老的方式去改变

我认为Vuex的使用还是比较繁琐的，比如像state，mutation，action等，所以在选型的时候对一下比较小的应用不会选择使用Vuex,一个简单的存储的对象就可以了，当然对于大的应用Vuex是必须的，当然也会来选择pinia

##### Vuex的五个核心模块

* state：存放状态的地方
* getters：某些属性我们可能需要经过变化后来使用，这个时候可以使用getters，有点像computed
* mutations：更改 Vuex 的 store 中的状态的唯一方法是提交 mutation，必须是同步的
* actions：Action类似于mutation，不同在于Action提交的是mutation，而不是直接变更状态；Action可以包含任意异步操作；
* module：允许将单一的 Store 拆分为多个 store 且同时保存在单一的状态树中。当应用变得非常复杂时，    store 对象就有可能变得相当臃肿为了解决以上问题，Vuex 允许我们将 store 分割成模块
  每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块

##### 你觉得Vuex有什么缺点

* Vuex的使用相对于redux已经相当方便了，但是在使用的过程中感觉模块话这一快比较复杂，容易出错，经常需要查看文档，对Vue3的支持非常的不好，对ts的支持也不好
* pinia出来之后 真的好用，我觉得Vue3+pinia是更好的组合

##### 补充：你有使用过Vuex的module吗？

* 用过module，随着我们的项目越来越大，单独的一个store对象会显得过于臃肿，通过模块化的方式可以拆分开来便于维护
* 可以按之前规则单独编写子模块代码，然后在主文件中通过`modules`选项组织起来：
* 不过使用时要注意访问子模块状态时需要加上注册时模块名
  * `store.state.模块名字.xxx`
  * 默认情况下，模块内部的`mutations`和`actions`仍然是注册在**全局命名空间**的，使用方式和之前一样，这样使得多个模块能够对同一个 action 或 mutation 作出响应
  * Getter 同样也默认注册在**全局命名空间**
  * 如果要做到完全拆分，需要在子模块加上`namespace`选项 设置为true，此时再访问它们就要加上命名空间前缀。
* 模块的方式可以拆分代码，但是缺点也很明显，就是使用起来比较繁琐复杂，容易出错，相比之下的pinia在这方面又很大的改进



### 5.2 什么是pinia?

* Pinia本质上依然是一个状态管理库
* Pinia开始于大概2019年，最初是为vue重新设计的状态管理，一个实验性的
* Pinia 最初是为了探索 Vuex 的下一次迭代会是什么样子，结合了 Vuex 5 核心团队讨论中的许多想法
* vue团队意识到Pinia已经实现了Vuex5中大部分内容，所以最终决定用Pinia来替代Vuex

##### pinia与Vuex的区别

* Pinia 提供了一个更简单的 API，提供了 Composition-API 风格的 API

* vuex在compositions-API中使用mapGetters，mapMutations等辅助函数会比较难以使用

  * 在compositions-API不推荐使用map辅助函数
  * 可以通过结构获取 -- 因为结构后不是响应式的 需要加上toRefs

  ```js
  const store = useStore();
  const { name, level } = toRefs(store.state);
  
  const store = useStore();
  const { message } = toRefs(store.getters);
  ```

* pinia中只有三大核心，state，getters，actions

  - mutations 不再存在，经常被认为是 非常冗长

* 不再有modules的嵌套结构

  - 可以灵活使用每一个store，它们是通过扁平化的方式来相互使用的

* 也不再有命名空间的概念，不需要记住它们的复杂关系

* 更友好的TypeScript支持，Vuex之前对TS的支持很不友好







## 6. Vue其他问题

### 6.1 什么是虚拟DOM?什么是diff算法?

##### 虚拟DOM

* Virtual DOM 本质上是 JavaScript 对象，是真实 DOM 的描述，⽤⼀个 JS 对象来描述⼀个 DOM 节点。
* Virtual DOM 可以看做⼀棵模拟 DOM 树的 JavaScript 树，当组件状态发⽣更新时，然后触发 Virtual DOM 数据的变化，然后通过 Virtual DOM 和真实 DOM 的⽐对，再对真实 DOM 更新。
  * 在vue/react当中我们不是直接去操作DOM的,而是通过数据来驱动视图的,操作DOM是交给框架来做的,这个时候就要有一种比较高效的方式来控制DOM的操作次数,vue/react采用的就是虚拟DOM

**虚拟DOM的优缺点**

* 优点
  * **跨平台与分层设计(主要原因)：**虚拟 DOM 最大的优势在于抽象了原本的渲染过程，实现了跨平台的能力，而不仅仅局限于浏览器的 DOM，可以是安卓和 IOS 的原生组件，可以是小程序。`React` 到 `Vue` ，虚拟 `DOM` 为这两个框架都带来了跨平台的能力`React-Native` 和 `Weex`
  * 操作真实DOM是很慢的,哪怕一个最简单的`div`也包含着很多属性,操作`DOM`的代价仍旧是昂贵的，频繁操作还是会出现页面卡顿，影响用户的体验
  * **将真实节点抽象成VNode,有效减少直接操作DOM的次数,从而提高性能**
  * 虚拟 DOM 可以将多次状态变化合并为一次更新，减少直接操作 DOM 的次数
  * **Virtual DOM 的优势不在于单次的操作，而是在大量、频繁的数据更新下，能够对视图进行合理、高效的更新**。为了实现⾼效的 DOM 操作， ⼀套⾼效的虚拟 DOM diff 算法显得很有必要
* 缺点
  * **内存占用**：虚拟 DOM 需要在内存中维护一棵树，可能会占用较多的内存。
  * **性能开销**：Diff 算法和虚拟 DOM 的创建和对比会带来一定的性能开销。
  * **不适合简单场景**：对于简单的应用或静态页面，虚拟 DOM 可能会带来不必要的复杂性。

**虚拟DOM的核心就是diff算法**

##### diff算法

```js
回答思路:
diff算法是干什么的?
# 是一种优化手段，将前后两个模块进行差异化比较
# vue中的diff算法有称作patching算法,它是由Snabbdom修改而来,vDOM想要转化为真实DOM就需要通过patch方法
他的必要性?
他何时执行?
具体执行方式?
说说vue3中的优化?
```

```js
传统Diff算法是循环递归每一个节点
# 在树形结构中递归遍历的时间复杂度是O(n的三次方)
将/*两颗树中所有的节点*/一一对比需要O(n²)的复杂度，在对比过程中发现旧节点在新的树中未找到，那么就需要把旧节点删除，删除一棵树的一个节点(找到一个合适的节点放到被删除的位置)的时间复杂度为O(n),同理添加新节点的复杂度也是O(n),合起来diff两个树的复杂度就是O(n³)
```

* diff算法并非Vue独家首创，优化了传统的diff算法 是⼀种通过**同层的树节点**进行比较的⾼效算法。
* diff 整体策略为：深度优先，同层比较。
  * 特点
    * 比较只会在同层级进行, 不会跨层级比较
    * 深度优先: 当发现两个节点都是元素 则 深度优先 先看双方子元素的情况

* 何时执行
  * vue组件在数据发生变更的时候 希望组件去更新 怎么更行呢?
  * 先通知这个组件 让它执行render(渲染)函数 render函数重行执行 得到最新的虚拟DOM
    * 执行patch函数 并传入新旧两次虚拟DOM
  * 得到虚拟DOM之后 并不知道程序什么地方发生了变化 这个时候就需要做比对
  * 于是 就把上一次的计算结果和这一次的计算结果进行一次diff过程 这就是diff算法
  * 在diff的过程 依据规则 找到前后变化的点  最后进行DOM操作
  * 虽然消耗了一些CPU的计算量 但是相对来讲在更新的时候执行效率就更高了
  * 哪里变化改哪里 而不是说一个变化整个视图都去变



### 6.2 Vue2 和Vue3的响应式原理

* 数据响应式 就是使数据变化可以被检测到,并对这种变化做出响应的机制
* MVVM框架中要解决的一个核心问题就是连接数据层和视图层
* vue中 通过数据响应式 + 虚拟DOM + patch算法(diff算法中 虚拟DOM想要转化成真实DOM就必须要通过patch方法)

**Vue2**

Vue.js 2.0 采⽤数据劫持并结合了发布者-订阅者模式，通过 Object.defineProperty()来劫持各个属性的 setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调

defineProperty必须循环遍历 data 中的属性 设置getter、setter 不管我们用不用 初识化的时候都要循环遍历 这样才能做数据响应式 这是一种浪费

对于数组而言 是通过覆盖数组的对象原型 而重新实现的方法

新增或删除属性需要使用Vue.set/delete这个的特殊api才能生效

对于es6中Set/Map这些数据结构不支持

**Vue3**

Vue.js 3.0放弃了Object.defineProperty API，⽽使⽤了更快的Proxy API。Proxy 是在 ES6 中引⼊，它允许你拦截对该对象的任何交互，也可以避免 Vue 早期版本中存在的⼀些响应性问题

| 实现原理 | defineProperty           | proxy                   | value setter      |
| -------- | ------------------------ | ----------------------- | ----------------- |
| 实际场景 | Vue2 响应式              | Vue3 reactive           | Vue3 ref          |
| 优势     | 兼容性                   | 基于Proxy实现真正的拦截 | 简单实现          |
| 劣势     | 数组和属性删除等拦截不了 | 兼容不了ie11            | 只拦截了value属性 |
| 实际应用 | Vue2                     | Vue3复杂数据结构        | Vue3 简单数据架构 |

3.2版本之后，现在ref确实是比reactive优先级更高一些，直接建议ref + toRefs一把梭，而且ref能够支持复杂的数据结构，也是调用了reactive



### 6.3 nextTick 方法的实现原理

* 定义

  * 在下次 DOM 更新循环结束之后执行延迟回调。**在修改数据之后立即使用这个方法，获取更新后的 DOM**
  * 因为Vue更新DOM是有策略的，不是同步更新，通过nextTick 可以获取到更新后的DOM --- 查看1.9

* 疑问?

  * 下次 DOM 更新循环结束之后?
  * 执行延迟回调?
  * 更新后的 DOM?

* 从上面三个疑问大胆猜想一下

  * vue 更新DOM是有策略的，不是同步更新
  * nextTick 可以接收一个函数做为入参
  * nextTick 后能拿到最新的数据

* nextTick 实现原理

  * 完全是基于js语言执行机制实现，直接创建一个异步任务，那么`nextTick`自然就达到在同步任务后执行的目的
  * 当调用nextTick时，nextTick内部会将回调函数使⽤Promise来包裹，⽬的是将该回调函数加⼊到微任务队列中
  * 队列的任务都是先进先出的，所以当执⾏完主程序的代码之后就会执⾏微任务队列中nextTick的回调函数，那这个过程就称为⼀次tick。

* 总结

  * `nextTick` 是 `vue` 中的DOM更新策略，**也是性能优化手段，基于`JS`执行机制实现**
  * `vue` 中我们改变数据时不会立即触发视图，如果需要实时获取到最新的`DOM`，这个时候可以手动调用 `nextTick`

  ```js
  回答范文
  nextTick方法 修改数据之后立即使用这个方法，可以获取更新后的 DOM
  因为Vue更新DOM是有策略的，不是同步更新，通过nextTick可以获取到更新后的DOM
  这和js的执行机制有关,我们知道js是单线程的
  单线程就意味着我们所有的任务都需要排队，后面的任务必须等待前面的任务完成才能执行
  如果前面的任务耗时很长，一些不需要等待的任务就会一直等待,这样肯定是不能接受的
  所以就出现了异步的概念
  同步任务在主线程上执行,形成一个执行栈 异步任务在一个"任务队列"中 一旦执行栈中的同步任务执行完了 就会读取"任务队列"中有那些事件,进入执行栈开始执行 主线程不断重复这几个步骤
  nextTick 实现原理 就是基于这个js语言执行机制实现的 直接创建一个异步任务 nextTick自然就达到在同步任务后执行的目的
  ```

  ```js
  用于vue中dom的更新是异步执行的，修改数据的使用视图不会立即更新，而是会监听数据的变化并缓存在同一事件循环中，等同一数据循环中所有的数据变化完成之后，再同意进行视图更新
  我们经常再dom还未更新的时候就使用了某个元素，这样是拿不到变更后的dom的
  所以为了能够得到更新后的dom，就设置了nextTick方法，再修改数据之后立即使用这个方法获取更新后的dom
  它主要是用于处理数据动态变化后，dom还未及时更新的问题
  
  在实际的项目中 在生命周期的created函数进行一些dom操作的时候，就一定要吧相应的代码逻辑写在nextTick的回调函数中，这是因为在created钩子函数中dom还未进行任何的渲染，此时进行dom操作是没有用的
  ```
  
  



### 6.4 Proxy 与 Object.defineProperty 优劣对比

* Object.defineProperty**只能劫持对象的属性**, 而 Proxy 是直接代理对象(直接监听对象而非属性)
* 由于 Object.defineProperty 只能对属性进⾏劫持，**需要遍历对象的每个属性**，**如果属性值也是对象，则需要深度遍历** --- 而 Proxy 直接代理对象，不需要遍历操作
* Vue2.x中的响应式实现正是基于defineProperty的, 对data中的属性做了遍历 + 递归，为每个属性设置了getter、setter。这也就是为什么 Vue 只能对 data 中预定义过的属性做出响应的原因
* Object.defineProperty**不能监听属性的新增和删除**
* `Proxy`有13中拦截方法
* * 而Object.defineProperty只能遍历对象属性直接修改
* `Proxy`作为新标准将受到浏览器厂商重点持续的性能优化
* `Proxy` 兼容性差 --- Object.defineProperty兼容性好（支持IE9）



### 6.5 使用过Vue SSR吗？说说SSR

* SSR (Server-Side Rendering) --- 服务端渲染
  * 由服务端形成的html ⽚段直接返回给客户端这个过程就叫做服务端渲染
* 可以说`Vue SSR`是一个在`SPA`上进行改良的服务端渲染

**SSR主要解决了以下两种问题**

* 更好的 SEO
  * 因为 SPA ⻚⾯的内容是通过 Ajax 获取，⽽搜索引擎爬取⼯具并不会等待 Ajax 异步完成后再抓取⻚⾯内容，所以在 SPA 中是抓取不到⻚⾯通过 Ajax 获取到的内容
  * ⽽ SSR 是直接由服务端返回已经渲染好的⻚⾯（数据已经包含在⻚⾯中），所以搜索引擎爬取⼯具可以抓取渲染好的⻚⾯
* ⾸屏加载更快(更快的内容到达时间)
  * SPA 会等待所有 Vue 编译后的 js ⽂件都下载完成后，才开始进⾏⻚⾯的渲染
  * SSR 直接由服务端渲染好⻚⾯直接返回显示，⽆需等待下载 js ⽂件及再去渲染

**服务端渲染的缺点**

* 更多的开发条件限制： 例如服务端渲染只⽀持 beforCreate 和 created 两个钩⼦函数
* 一些外部库可能需要特殊处理才能在服务端渲染的应用中运行。
* 更多的与构建配置和部署相关的要求。服务端渲染的应用需要一个能让 Node.js 服务器运行的环境，不像完全静态的 SPA 那样可以部署在任意的静态文件服务器上。
* 更高的服务端负载。相对于前后端分离服务器只需要提供静态资源来说，服务器负载更大，所以要慎重使用

所以在我们选择是否使用`SSR`前，我们需要慎重问问自己这些问题：

1. 需要`SEO`的页面是否只是少数几个，这些是否可以使用预渲染（Prerender SPA Plugin）实现
2. 首屏的请求响应逻辑是否复杂，数据返回是否大量且缓慢



### 6.6 你对Vue项目进行那些优化？



### 6.7 如何实现Vue首屏加载优化的

* 正常来说，首屏加载时间不应该超过2s~3s

* 面渲染的过程，导致加载速度慢的因素可能是
  * 网络延时问题
  * 资源文件体积是否过大
  * 资源是否重复发送请求去加载了
  * 加载脚本的时候，渲染内容堵塞了

**优化方案**

* 减小入口文件积
  * 常用的手段是路由懒加载，把不同路由对应的组件分割成不同的代码块，待路由被请求的时候会单独打包路由，使得入口文件变小，加载速度大大增加
* 静态资源本地缓存
* UI框架按需加载
  * 例如`element-UI`、或者`ant design`
* 图片资源的压缩 / 图片使用懒加载
  * 图片资源虽然不在编码过程中，但它却是对页面性能影响最大的因素
  * 对于所有的图片资源，我们可以进行适当的压缩
  * 对页面上使用到的`icon`，可以使用在线字体图标，或者雪碧图，将众多小图标合并到同一张图上，用以减轻`http`请求压力
  * 通过给img标签加上loading="lazy来开启懒加载模式。或者UI库也有提供图片懒加载的组件
* 使用SSR服务端渲染
* keep-alive 缓存组件: 避免重复创建组件实例 且能保留缓存组件的状态
* 引入http2.0。http2.0对比http1.1，最主要的提升是传输性能，在接口小而多的时候性能优势会更加明显。
* 适当的组件的拆分: 但同时也不宜过渡的拆分 组件实例的消耗远大于纯DOM节点
* **前端页面代码层面的优化**
  * 合理使用v-if和v-show
  * 合理使用watch和computed
  * 避免将v-if和v-for写在一起
  * vue3中新增的指令v-memo 仅供性能敏感场景的针对性优化, 指定数据不变的话 列表将不会被重新渲染
  * 使用v-for必须添加key, 最好为唯一id



### 6.8 Vue3.0 里为什么要用 Proxy API替代 defineProperty API？

* defineProperty API 的局限性最⼤原因是它只能针对对象的属性做监听。
  * Vue2.x中的响应式实现正是基于Object.defineProperty来实现，对 data 中的属性做了遍历 + 递 归，为每个属性设置了 getter、setter。这也就是为什么 Vue 只能对 data 中预定义过的属性做出响应的原因
  * 检测不到对象属性的添加和删除
  * 数组`API`方法无法监听到
  * 需要对每个属性进行遍历监听，如果嵌套对象，需要深层监听，造成性能问题
* Proxy API监听是针对⼀个对象的，那么对这个对象的所有操作会进⼊监听操作， 这就完全可以代理所有属性，将带来很⼤的性能提升和更优的代码
  * `Proxy`直接可以劫持整个对象，并返回一个新对象，我们可以只操作新的对象达到响应式目的
* 正因为`defineProperty`自身的缺陷，导致`Vue2`在实现响应式过程需要实现其他的方法辅助（如重写数组方法、增加额外`set`、`delete`方法）



### 6.9 说说你的vue项目的目录结构，如果是大型项目你该怎么划分结构和划分组件呢？

项目结构清晰会提高开发效率 在划分项目结构的时候，需要遵循一些基本的原则：

* 单一的出入口 -- 通过 文件夹/index.js 作为改文件夹的唯一入口
* 就近原则，耦合度高的文件应该放到一起 使用相对路径 -- ./home/index.vue
* 公共的文件应该以绝对路径的方式从根目录引用 -- @/components
* 一些公共的组件一般是放到src/components文件夹下
* store / router 放状态管理库和路由
* css和图片资源我会放在src/assets文件夹下 css和img文件夹 并且css由index.css同意导出(公共样式和重置样式)
* 等等



### 6.10 vue要做权限管理该怎么做？如果控制到按钮级别的权限怎么做？

- **角色（Role）**：用户的身份标识，如管理员、普通用户等。
- **按钮级别权限（Permission）**：具体的操作或访问权限，如“创建用户”、“删除文章”等。
- **路由权限**：控制用户能够访问哪些页面。
- **功能权限**：控制用户能够在页面上执行哪些操作。
- **数据权限**：控制用户能够访问哪些数据。

- 根据用户的权限信息动态的添加路由(而不是一次性的注册所有路由)

- 方案一: 基于角色(Role)的动态路由管理

  - 在我们前端这边定义好 有哪些角色

  ```js
  const roles = {
      superadmin: [写所有的路由] => 将这些路由添加到router.addRoute('main', superadmin)
      admin: [一部分内容]
      service: [少部分路由]
  }
  弊端: 每增加一个路由,都要增加key/value
   1.若前端代码已经发布出去了,需要将key/value写到roles中,并重新发布代码
   2.或者让后端放回roles对象 但是后端不好组织roles对象的
  ```

- 方案二: 基于菜单(menu)的动态路由管理

  - useMenus => 动态展示菜单
  - 根据登录角色返回的菜单 动态添加路由

##### 根据菜单动态的添加路由对象 (在独立文件中)

- 获取菜单 useMenus
- 动态的获取所有的路由对象(都在router/main中),放到数组中
  - 路由对象都在独立的文件中
  - 从文件中将所有的路由对象读取到数组中
- 根据菜单匹配正确的路由
  - router.addRoute('main', xxxxxx)

##### 解决页面刷新后动态添加的路由没有 --- 用户刷新后需要加载默认数据



##### 进入main页面后匹配第一个路由



##### 刷新页面后需要根据path匹配要显示的菜单

- 就是刷新后保持菜单在原来的地方,不能还是进入main后的第一个菜单



### 6.11 说说vue中刷新页面的方式

* location.reload() / this.$router.go(0) 强制刷新



### 6.12 说说你对前端组件化和模块化的理解

* 主要通过根据划分的角度不同来区分
* 组件化是从UI的角度划分的
  *  页面上每个独立的区域都可以看作是一个组件
  * 前端组件话开发能够便于组件的复用
* 模块化是从代码逻辑的角度划分的，保证每个模块的只能单一
  * 比如登录页的登录功能是一个模块,注册功能又算是一个模块

###### 组件化开发

* 我们会把组件分成两个类型
  * 通用型组件 - 就是各大组件库的组件风格，包括按钮、表单、弹窗等通用功能
  * 业务型组件 - 业务的交互逻辑，包括购物车、登录注册等 就是我们当前项目要使用的组件
* 组件的开发由于要考虑代码的复用性，会比通常的业务开发要求更高，需要有更好的可维护性和稳定性的要求。
*  组件设计其实就是props，event和slot三个方法考虑，是否要抽离出组件需要看复用的需求

###### 前端工程化

* 主要目的: 为了提高效率和降低成本（即提高开发过程中的开发效率，减少不必要的重复工作时间）



### 6.13 Vue样式模块化 scoped

* 当组件添加上scoped后,会给这个组件的所有标签元素添加一个唯一标识 [ data-v-xxxx ] 
* 这个唯一标识就是 "自定义属性" ,同时,对应的样式选择器也会添加上这个唯一的属性选择器
* 由于每个组件的标识都是唯一的, 所以不会有重复的属性选择器出现
* 这样就能够做到样式隔离



### 6.14 异步组件是什么？使用场景有哪些？

* 随着项目的增大，可能需要将应用分割为更小的块，并且在需要时再加载它们

* 我们不仅可以在路由切换时懒加载组件，还可以在页面组件中继续使用异步组件，从而实现更细的组件分割

* 使用异步组件最简单的方式是直接给defineAsyncComponent指定一个函数，结合import可以快速实现

  ```js
  const AsyncCategory = defineAsyncComponent(() => import("./views/Category.vue"));
  ```

* 异步组件容易和路由懒加载混淆，实际上不是一个东西

  * 异步组件不能用在定义路由懒加载上，处理它的是vue框架，处理路由组件加载的是vue-router
  * 但是可以在懒加载的路由组件中使用异步组件



### 6.15 使用vue渲染大量数据时应该怎么优化？说下你的思路！

* 当项目比较大时，经常需要渲染大量数据，此时很容易出现卡顿的情况。比如大数据量的表格、树

* 这个时候要根据情况做不通处理：
  * 可以采取分页的方式获取，避免渲染大量数据
  * 如果不需要更新，可以使用`v-once`方式只渲染一次
  * Vue3的新增指令v-memo可以缓存结果，结合v-for使用，避免数据变化时不必要的VNode创建
  * 虚拟滚动插件`vue-virtual-scroller`，只渲染视口范围内的数据
  * 可以采用懒加载方式，在用户需要的时候再加载数据，比如tree树组件的懒加载
  
* 总之，还是要看具体需求，首先从设计上避免大数据获取和渲染；实在需要这样做可以采用虚表的方式优化渲染；最后优化更新，如果不需要更新可以v-once处理，需要更新可以v-memo进一步优化大数据更新性能。其他可以采用的是交互方式优化，无线滚动、懒加载等方案

* 虚拟滚动方案

  ```js
  - 1.使用第三方库实行虚拟列表 `vue-virtual-scroller`
  - 2.手动实现虚拟列表时，结合 `v-for` 和动态样式计算可见区域的数据。
  ```

  * 虚拟列表如何复用dom?
    * 使用 `v-for` 渲染可见区域的数据，并通过 `key` 属性确保 Vue 复用 DOM 节点。
    * 当用户滚动时，动态更新 `visibleData`，Vue 会自动复用 DOM 节点并更新内容，而不是销毁和重新创建
  * 为什么呢? 就要说一下vue中key的作用了
  * key主要作用是帮助 Vue 识别哪些节点是新的、哪些节点是已经存在的，从而决定是否需要创建、更新或删除 DOM 节点。
    * 当 `key` 相同时，Vue 会认为这是同一个节点，并尝试复用该节点。
    * 当 `key` 不同时，Vue 会认为这是一个新节点，可能会销毁旧节点并创建新节点
  * Vue 使用 **虚拟 DOM** 来高效地更新真实的 DOM。当数据发生变化时，Vue 会生成一个新的虚拟 DOM 树，并与旧的虚拟 DOM 树进行比较（这个过程称为 **Diff 算法**）。通过比较，Vue 可以确定哪些节点需要更新、哪些节点可以复用。
  * 在 `v-for` 渲染列表时，Vue 会根据 `key` 来判断节点的身份：
    - 如果 `key` 相同，Vue 会复用该节点，并更新其内容。
    - 如果 `key` 不同，Vue 会销毁旧节点并创建新节点。
  * vue为什么会自动复用呢?
  * 在虚拟列表的实现中，`visibleData` 是根据滚动位置动态计算的。当用户滚动时，`visibleData` 会发生变化，但大部分数据的 `key` 并不会改变（因为数据是连续的，只是起始索引和结束索引发生了变化）。例如：
    - 初始时，`visibleData` 包含 `[Item 0, Item 1, Item 2, Item 3, Item 4]`。
    - 用户滚动后，`visibleData` 变为 `[Item 1, Item 2, Item 3, Item 4, Item 5]`。

* 懒加载方式

  * 使用 `IntersectionObserver` API 监听元素是否进入可视区域

  * 结合 Vue 的 `v-if` 或 `v-show` 动态加载数据

  *  `IntersectionObserver` API它可以高效地检测元素是否进入或离开可视区域，而无需频繁地监听滚动事件

  * 在传统的实现中，检测元素是否进入可视区域通常需要：

    - 监听 `scroll` 事件。
    - 使用 `getBoundingClientRect` 计算元素的位置。
    - 频繁触发回调，可能导致性能问题。

  * `IntersectionObserver` 解决了这些问题：
- **异步执行**：回调函数在浏览器空闲时执行，不会阻塞主线程。
    - **高效检测**：浏览器内部优化了交叉状态的计算，性能更高。
    - **简单易用**：只需配置观察器和回调函数即可。
    
  ```js
  const observer = new IntersectionObserver((entries, observer) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        console.log('元素进入可视区域');
      } else {
        console.log('元素离开可视区域');
      }
    });
  });
  ```
  
  



### 6.16 jsx与template

* template 的语法是固定的，只有 v-if、v-for 等等语法，也就是说，template 遇见条件渲染就是要固定的选择用 v-if。我们按照这种固定格式的语法书写，这样 Vue 在编译层面就可以很方便地去做静态标记的优化。

  * 而 JSX 只是 h 函数的一个语法糖，本质就是 JavaScript，想实现条件渲染可以用 if else，也可以用三元表达式，还可以用任意合法的 JavaScript 语法

* 也就是说，JSX 可以支持更动态的需求。而 template 则因为语法限制原因，不能够像 JSX 那样可以支持更动态的需求。这是 JSX 相比于 template 的一个优势。

* JSX 相比于 template 还有一个优势，是可以在一个文件内返回多个组件，

  ```jsx
  export const Button = (props,{slots})=>slots.default()
  export const Input = (props)=><input {...props} />
  export const Timeline = (props)=>{ ...}
  ```

* template 由于语法固定，可以在编译层面做的优化较多，比如静态标记就真正做到了按需更新；

* h 函数，简单来说，h 函数内部执行 createVNode，并返回虚拟 DOM，而 JSX 最终也是解析为 createVnode 执行。而在一些动态性要求很高的场景下，很难用 template 优雅地实现，所以我们需要 JSX 实现



### 6.17 如何封装一个组件

* 说的组件要难一点 最好要涉及`slot` `组件通信`
* 组件分为 业务型组件 / 通用型组件

##### 基于element的二次封装

* table
* form



### 6.18 Vue中给对象添加新属性时界面不会刷新?

```js
data() {
  obj: {
    oldProperty:"旧属性"
  }
}
methods: {
  feat() {
    this.obj.newProperty = "新属性" // 为obj添加新属性
    console.log(this.obj)
  },
},
```

* 点击按钮，发现结果不及预期，数据虽然更新了（`console`打印出了新属性），但页面并没有更新

* 原理

  * `vue2`是用过`Object.defineProperty`实现数据响应式

  ```js
  const obj = {}
  Object.defineProperty(obj, 'foo', {
          get() {
              console.log(`get foo:${val}`);
              return val
          },
          set(newVal) {
              if (newVal !== val) {
                  console.log(`set foo:${newVal}`);
                  val = newVal
              }
          }
      })
  }
  ```
  * 当我们访问`foo`属性或者设置`foo`值的时候都能够触发`setter`与`getter`
  * 但是我们为`obj`添加新属性的时候，却无法触发事件属性的拦截
  * 原因是一开始`obj`的`foo`属性被设成了响应式数据，而`bar`是后面新增的属性，并没有通过`Object.defineProperty`设置成响应式数据

* 解决方案

  * Vue.set()
    * Vue.set()的源码, 调用了一个`defineReactive`方法，实现新增属性的响应式
    * `defineReactive`方法，内部还是通过`Object.defineProperty`实现属性拦截
  * Object.assign()
    * 直接使用`Object.assign()`添加到对象的新属性不会触发更新
    * 应创建一个新的对象，合并原对象和混入对象的属性
  * $forceUpdate
    * 实在不知道怎么操作时，可采取`$forceUpdate()`进行强制刷新 (不建议)

**PS: `vue3`是用过`proxy`实现数据响应式的，直接动态添加新属性仍可以实现数据响应式**



### 6.19 Vue项目本地开发完后部署到服务器后报404是什么原因?

前端打包后上传到服务器, 让web跑起来, 以nginx为例

```js
server {
  listen  80;
  server_name  www.xxx.com;

  location / {
    index  /data/dist/index.html;
  }
}
```

```js
// 检查配置是否正确
nginx -t 

// 平滑重启
nginx -s reload
```

* 场景还原

  * `vue`项目在本地时运行正常，但部署到服务器中，刷新页面，出现了404错误
  * HTTP 404 错误意味着链接指向的资源不存在

* 为什么history模式下有问题?

  * `Vue`是属于单页应用
  * SPA页面, 所有用户交互是通过动态重写当前页面, 不管我们应用有多少页面，构建物都只会产出一个`index.html`
  * 可以根据 `nginx` 配置得出，当我们在地址栏输入 `www.xxx.com` 时，这时会打开我们 `dist` 目录下的 `index.html` 文件，然后我们在跳转路由进入到 `www.xxx.com/login`
  * 当我们在 `xxx.com/login` 页执行刷新操作，`nginx location` 是没有相关配置的，所以就会出现 404 的情况

* 为什么hash模式下没有问题?

  * `hash` 模式我们都知道是用符号#表示的，如 `xxx.com/#/login`, `hash` 的值为 `#/login`
  * 它的特点在于：`hash` 虽然出现在 `URL` 中，但不会被包括在 `HTTP` 请求中，对服务端完全没有影响，因此改变 `hash` 不会重新加载页面
  * `hash` 模式下，仅 `hash` 符号之前的内容会被包含在请求中，如 `website.com/#/login` 只有 `website.com` 会被包含在请求中 ，因此对于服务端来说，即使没有配置`location`，也不会返回404错误

* 解决方案

  * 产生问题的本质是因为我们的路由是通过JS来执行视图切换的
  * 当我们进入到子路由时刷新页面，`web`容器没有相对应的页面此时会出现404
  * 所以我们只需要配置将任意页面都重定向到 `index.html`，把路由交由前端处理

  ```js
  server {
    listen  80;
    server_name  www.xxx.com;
  
    location / {
      index  /data/dist/index.html;
      try_files $uri $uri/ /index.html;
    }
  }
  ```

  * 修改完配置文件后记得配置的更新

  ```js
  nginx -s reload
  ```

  * 为了避免这种情况，你应该在 `Vue` 应用里面覆盖所有的路由情况，然后在给出一个 404 页面

  ```js
  const router = new VueRouter({
    mode: 'history',
    routes: [
      { path: '*', component: NotFoundComponent }
    ]
  })
  ```

  







## 7. axios网络请求库

### 7.1 axios是什么？怎么使用？怎么解决跨域？与ajax的区别

**axios是什么**

* Axios 是⼀个基于 promise 的 HTTP 请求库，可以⽤在浏览器和 node.js 中。
* 前端最流⾏的 ajax 请求库， react/vue 官⽅都推荐使⽤ axios 发 ajax 请求

**axios的特点**

* 基于 promise 的异步 ajax 请求库，⽀持promise所有的API
* 浏览器端/node 端都可以使⽤，浏览器中创建XMLHttpRequests
* ⽀持请求／响应拦截器
* ⽀持请求取消 
* JSON数据的⾃动转换
* 批量发送多个请求
* 安全性更⾼，客户端⽀持防御 XSRF
  * 就是让你的每个请求都带⼀个从cookie中拿到的key, 根据浏览器同源策略，假冒的⽹站是拿不到你cookie中得key的，这样，后台就可以轻松辨别出这个请求是否是⽤户在假冒⽹站上的误导输⼊， 从而采取正确的策略。

##### axios与ajax的区别

* 两者本质上没有什么区别，axios就是通过promise实现的对ajax技术的一种封装

##### ajax的原理

* Ajax的原理简单来说**通过XmlHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用javascript来操作DOM更新页面**。 

**常用语法**

* axios(confifig): 通⽤/最本质的发任意类型请求的⽅式 
* axios.request(confifig): 等同于 axios(confifig) 
* axios.get(url[, confifig]): 发 get 请求 
* axios.post(url[, data, confifig]): 发 post 请求 
* axios.defaults.xxx: 请求的默认全局配置 
* axios.interceptors.request.use(): 添加请求拦截器 
* axios.interceptors.response.use(): 添加响应拦截器 
* axios.create([confifig]): 创建⼀个新的 axios(它没有下⾯的功能) 
* axios.CancelToken(): ⽤于创建取消请求的 token 对象

**开发环境重解决跨域**

* ⽅式⼀：在vue.config.js中的devServer选项中的proxy中配置反向代理 
* ⽅式⼆：在vite.config.js中的server选项中的proxy中配置反向代理 
* ⽅式三：直接后端开发⼈员配置cors

**部署的时候解决跨域**

* ⽅式⼀：直接后端开发⼈员配置cors 
* ⽅式⼆：反向代理，⽐如：nginx 服务器的反向代理

##### 补充：ajax、fetch 、axios的区别

* **ajax**（Async Javascript And XML）异步 JavaScript 和XML
  * 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术
  * 缺点
    * 本身是针对 MVC 编程，不符合前端 MVVM 的浪潮
    * 基于原生 XHR （XMLHttpRequest）开发，XHR 本身的架构并不清晰

* **fetch**
  * Fetch API是`XMLHttpRequest`的替代方案
  * Fetch 是基于 promise 设计的，Fetch 的代码结构比起 ajax 简单多
  * fetch 不是 ajax 的进一步封装，而是原生 js，没有使用 XMLHttpRequest 对象
  * 优点：
    * 语法简洁，更加语义化
    * 基于标准 Promise 实现，支持 async/await
    * 更加底层，提供的 API 丰富（request, response）
  * 缺点：
    * fetch 只对网络请求报错，对 400，500 都当做成功的请求，服务器返回 400，500 错误码时并不会 reject，只有网络错误这些导致请求不能完成时，fetch 才会被 reject
* **axios**



### 7.2 Vue项目中有封装过axios吗？主要是封装哪方面的？

* 随着项目规模增大，如果每发起一次`HTTP`请求，就要把这些比如**设置超时时间、设置请求头、根据项目环境判断使用哪个请求地址、错误处理等等**操作，都需要写一遍
* 这种重复劳动不仅浪费时间，而且让代码变得冗余不堪，难以维护
* 为了提高我们的代码质量，我们应该在项目中二次封装一下 `axios` 再使用

**如何封装**

在封装的同时,需要和 后端协商好一些约定，请求头，状态码，请求超时时间.......

设置接口请求前缀：根据开发、测试、生产环境的不同，前缀需要加以区分

请求头 : 来实现一些具体的业务，必须携带一些参数才可以请求

状态码: 根据接口返回的不同`status` ， 来执行不同的业务，这块需要和后端约定好

请求方法：根据`get`、`post`等方法进行一个再次封装，使用起来更为方便

请求拦截器: 根据请求的请求头设定，来决定哪些请求可以访问

响应拦截器： 这块就是根据 后端 返回来的状态码判定执行不同业务

###### 设置接口请求前缀

* 利用`node`环境变量来作判断，用来区分开发、测试、生产环境

```js
if (process.env.NODE_ENV === 'development') {
  axios.defaults.baseURL = 'http://dev.xxx.com'
} else if (process.env.NODE_ENV === 'production') {
  axios.defaults.baseURL = 'http://prod.xxx.com'
}
```

* 在本地调试的时候，还需要在`vue.config.js`文件中配置`devServer`实现代理转发，从而实现跨域

```js
devServer: {
    proxy: {
      '/proxyApi': {
        target: 'http://dev.xxx.com',
        changeOrigin: true,
        pathRewrite: {
          '/proxyApi': ''
        }
      }
    }
  }
```

###### 设置请求头与超时时间

* 大部分情况下，请求头都是固定的，只有少部分情况下，会需要一些特殊的请求头

###### 封装请求方法

###### 请求拦截器

```js
axios.interceptors.request.use(
    config => {
        // 每次发送请求之前判断是否存在token
        // 如果存在，则统一在http请求的header都加上token，这样后台根据token判断你的登录情况，此处token一般是用户完成登录后储存到localstorage里的
    },
    err => {
        
    }
)
```

###### 响应拦截器

```js
axios.interceptors.response.use(
    response => {
        // 如果返回的状态码为200，说明接口请求成功，可以正常拿到数据
  		// 否则的话抛出错误
    },
    err => {
        
    }
)
```







## 8. Vue VS React

### 8.1  Vue和React有什么不同？使用场景分别是什么？

* 相同点
  * 都有组件化思想
  * 都支持服务器端渲染
  * 都有Virtual DOM（虚拟dom）
  * 数据驱动视图
  * 都有自己的构建工具：`Vue`的`vue-cli`、`React`的`Create React App`
  * 都将diff算法的的时间复杂度优化到O (n) --- 传统的diff算法是O (n³) 
* 区别
  * React 的特⾊在于**函数式编程**的理念和丰富的技术选型
  * 核心思想不同
    * Vue在早期就尤雨溪槛，定位就是尽可能的降低前端开发的门槛，让更多的人能够更快地上手开发
    * React 从一开始的定位就是提出 UI 开发的新思路 用更好的方式去颠覆前端开发方式 推崇函数式编程
  * 数据流向的不同。`react`从诞生开始就推崇单向数据流，而`Vue`是双向数据流
    * react实现双向可以手动通过 同时绑定 `value` `onChange` (受控组件) 然后通过setState
  * diff算法不同。`react`主要使用diff队列保存需要更新哪些DOM，得到patch树，再统一操作批量更新DOM。`Vue` 使用双向指针，边对比，边更新DOM

**使用场景**

* React：适合构建大型应用程序，其函数编程让React开发应⽤时非常的灵活，并且React对TS⽀持非常的友好，也有非常大的生态系统。 

* Vue：适合使用模板搭建小而快的应用；适合简单、对灵活度要求没那么高的应用。自从Vue3出来后，对TS⽀持也越来越友好，⽣态系统也在慢慢的完善起来了。



## 9. Vue3

### 9.1 Vue3 与 Vue2的区别? / Vue3性能提升主要是通过哪几个方面体现的?

* 首先它们响应式实现原理

  * `vue2` 的响应式主要是基于 `Object.defineProperty` 进行实现，但是这个api只能监听对象的getter和setter行为，在一些情况下就会出现问题，比如我们在data中声明了一个对象，但是后面我们要给这个对象新增一些属性，那么这个新的属性就会失去响应性，不过我们可以通过$set的方式给它恢复响应性
  * `vue3`则是通过`proxy`来实现的，就不会有这样的问题，vue3中这个过程是通过`reactive`这个方法体现的，但是 proxy 只能实现代理复杂数据类型，所以vue额外提供了 `ref` 方法，通过 set 和 get 标记了 value 函数，以此来实现的，但是ref也能够支持复杂的数据结构，因为里面是调用了reactive，所以在开发中一般是ref一把梭哈

* 打包优化

  * Tree-shaking：webpack、rollup 等中的概念。是一种通过清除多余代码方式来优化项目打包体积的技术
* 主要依赖于 import 和 export 语句，用来检测代码模块是否被导出、导入，且被 JavaScript 文件使用。
  *  Vue2：以 nextTick 为例子，全局API暴露在Vue实例上，即使未使用，也无法通过 tree-shaking 进行消除。
* Vue3：中针对全局和内部的API进行了重构，并考虑到 tree-shaking 的支持
  * Vue 3 的核心库体积比 Vue 2 小约 40%。

- TypeScript支持

  - Vue3 由 TypeScript 重写，相对于 Vue2 有更好的 TypeScript 支持

- composition Api

  - Vue3在兼顾Vue2的options API的同时，还推出了composition API，大大增加了代码的逻辑组织和代码复用能力

- 其他小的改变

  - 生命周期
    - destroyed，beforeDestroy 生命周期选项被重命名为 unmounted，beforeUnmount
    - 没有beforeCreate 和 created，因为setup 是围绕这两个生命周期钩子运行的
  - vue3异步组件可以通过 defineAsyncComponent 方法来创建

  - Vue3组件现在支持有多个根节点 -- （Fragment）

  * Vue 3 提供了 `<teleport>` 组件，可以将子组件渲染到 DOM 中的任意位置。

    ```html
    <teleport to="body">
      <div class="modal">这是一个模态框</div>
    </teleport>
    ```

  - 组件上 v-model 用法已更改 -- Vue 3 支持多个 `v-model` 绑定

    ```js
    <my-component v-model:title="title" v-model:content="content" />
    ```

  - 在同一元素上使用的 v-if 和 v-for 优先级已更改

- 其他

  - 虚拟DOM -- Vue3 相比于 Vue2，虚拟DOM上增加 patchFlag 字段
  - 事件缓存
  - diff算法优化
    - Vue3在diff算法中相比Vue2增加了静态标记
    - 关于这个静态标记，其作用是为了会发生变化的地方添加一个`flag`标记，下次发生变化的时候直接找该地方进行比较
    - 已经标记静态节点在`diff`过程中则不会比较，把性能进一步提高
  - 静态提升
    - Vue3中对不参与更新的元素，会做静态提升，只会被创建一次，在渲染时直接复用
    - 这样就免去了重复的创建节点，免去了重复的创建操作，优化了运行时候的内存占用

* 打印proxy方法 const info = { ...proxy }



### 9.2 说说Vue 3.0中Treeshaking特性？举例说明一下？

* Tree shaking 是一种通过清除多余代码方式来优化项目打包体积的技术
* 简单来讲，就是在保持代码运行结果不变的前提下，去除无用的代码
* 在`Vue2`中，无论我们使用什么功能，它们最终都会出现在生产代码中。
* 而`Vue3`源码引入tree shaking特性，将全局 API 进行分块。如果不使用其某些功能，它们将不会包含在我们的基础包中

通过Tree shaking，Vue3给我们带来的好处是：

- 减少程序体积（更小）
- 减少程序执行时间（更快）

**在 Vue 2 中**，由于 Vue 的源代码是使用 CommonJS 格式编写的，所以它**不支持 tree shaking**。这意味着即使你只使用了 Vue 的一部分功能，你的最终打包文件仍然会包含整个 Vue 库的代码。

**在 Vue 3 中**，Vue 的源代码被重写为使用 ES Modules 格式，这使得 Vue 3 **支持 tree shaking**。这意味着如果你只使用了 Vue 的一部分功能，那么你的最终打包文件只会包含你实际使用的那部分代码，未使用的代码会被移除。



## 10 Vue3源码面试题















