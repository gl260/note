## 1. HTML标签有哪些行内元素

* i
* a
* img
* input
* span
* label
* select
* textarea



## 2. 说说你对元素语义化的理解

就是正确的元素做正确的是

比如

p标签就就用来写段落 h标签就用来写标题

元素语义化在实际开发中有很多好处

* 提高代码可阅读性 可维护性
* 减少程序员之间的沟通成本,提高团队开发和维护
* 有利于SEO
* 能让语音合成工具正确识别网页元素的用途，以便做出正确的反应



## 3. HTML有哪些语义化标签

* header
* footer
* aside
* article
* section
* address
* h1~h6
* p
* strong
* ...



## 4. 什么是URL编码

当 URL 路径，或者查询参数中带有中文、特殊字符的时候，就需要对 URL 进行编码（采用十六进制编码格式）

URL 之所以需要编码，是因为 URL 中的某些字符会引起歧义，比如若 URL 查询参数中包含”&”或者”%”就会造成服务器解析错误，再比如，URL 的编码格式采用的是 ASCII 码而非 Unicode，这表明 URL 中不允许包含任何非 ASCII 字符（比如中文），否则就会造成 URL 解析错误。



## 5. 说说你对SEO的理解

SEO就是搜索引擎优化(Search Engine Optimization)

SEO通过了解搜索引擎的运行规则来调整网站，以提高网站的曝光度,以及网站的排名

* 能采取哪些措施来进行SEO呢？
  * 目前国内针对百度来说有一个很直接的方式就是给钱
* 方式一：SSR服务端渲染
  * 我们现在的一些项目 大都是市基于vue/react进行开发的
  * 这种单页面应用（SPA）的内容是通过 Ajax 获取，而搜索引擎爬取⼯具并不会等待 Ajax 异步完成后再抓取页面内容，所以在 SPA 中是抓取不到页面通过 Ajax 获取到的内容
  * 而 SSR 是直接由服务端返回已经渲染好的页面（数据已经包含在页面中），所以搜索引擎爬取⼯具可以抓取渲染好的页面
* 方式二：准确的TDK描述
  * TDK就是 title/description/keywords
  * title标题：就是网站的标题，不仅用户会看到，搜索引擎通常会首先检索和收录title信息
  * description描述：通常在搜索引擎结果页中标题下方显示，描述网站内容
  * keywords关键词：这是网站中重要的词汇，反应了页面的主题和内容，每个关键字都要有对应的内容匹配。
* 方式三：语义化的HTML元素，图片alt,h1,h2的合理使用
  * **语义化的HTML代码**和**符合W3C规范**也是SEO的关键要素之一
  * 图片必须要求加alt，一方面图片无法显示时用户可以看到提示，另一方面也有利于SEO优化
* 方式四：编写合理的robots.txt文件
  * robots.txt是一个存放在网站根目录中的文本文件，主要作用就是告诉搜索引擎爬虫那些部分可以爬取，那些部分不能被爬取
  * 为什么要使用robots.txt：通过指示搜索引擎**忽略不重要的文件或目录**，让它**更专注于重要内容的爬取和索引**
  * 所以不编写robots.txt，可能会降低网站的SEO效率
  * 知乎：https://www.zhihu.com/robots.txt
  * 网易云音乐：
* 方式五：HTTPS
  * 自2014年以来，Google已将HTTPS作为搜索排名的信号之一
  * HTTPS也有利于用户的安全



## 6. **'+'** **与** **'~'** 选择器有什么不同

* `+` 相邻兄弟选择器
* `~` 普遍兄弟选择器 注意: 这里只会选择后面的元素,在前面的不会被选中





## 7. 说明text-align居中的条件

* text-align: center  必须要要是`行内级(inline-level)`元素
* 比如:  一般的文本, span, img
* 如果块级元素需要使用这个属性居中,则要将其设置为行内块级元素: `display:inline-block`





## 8. line-height为什么可以让文字垂直居中？

* 行高就是上下两个基线之间的距离
* 元素的整体高度 = 行高
* (行高 - font-size所设置的高度)   它两的差(也就是行距)会平分给文本内容的顶部和底部
  - 比如:一个盒子的高度是200px
  - 里面的font-size设置为16px,line-height:200px
  - (200 - 16) / 2 =92    它的顶部和底部都能分到92px





## 9.说说盒子模型包含哪些内容？

盒模型包含四部分: content padding border margin

- content: 内容

  - 内容是通过宽高设置的(行内非替换元素设置宽高是无效的)

- padding: 内边距

  - padding用来设置盒子内边距,是边框和内容之间的距离

- border: 边框

  - border用于设置盒子的边框,可以设置盒子边框的宽度,样式,颜色

  - ```css
    border: 1px solid #000;
    ```

  - 可以通过border-radius设置边框圆角

- margin: 外边距

  - margin用于设置盒子的外边距,通常是元素和元素之间的距离

**box-sizing是用来设置盒子宽高的行为(就是设置标椎盒模型和IE盒模型)**

- content-box: 所设置的宽高是:  内容 -- 标椎盒模型
  - 设置padding和border会将盒子撑大
- border-box:  所设置的宽高是: 内容+padding+margin -- IE盒模型
  - 设置padding和border不会将盒子撑大





## 10. 说说你对margin的传递和折叠的理解

**margin的传递**⼀般是父子块元素之间,有margin-top传递,margin-bottom传递

* margin-top传递
  * 如果块级元素的顶部线和父元素的顶部线重叠，那么这个块级元素的margin-top值会传递给父元素
  * 有几种解决办法
    * 1: 给父元素一个border(但是这样border会占用空间)
    * 2: 激活父元素的BFC(后面有) overflow: auto
    * 3: 给父元素设置padding-top/padding-bottom
* margin-bottom传递
  *  如果块级元素的底部线和父元素的底部线重叠，并且父元素的高度是auto，那么这个块级元素的margin-bottom值会传递给父元素

**margin的折叠**

- 垂直方向:  的两个相邻margin会合成为一个,这两个margin值会进行比较,取较大的值
- 水平方向:  不会层叠,两个margin会相加





## 11. **CSS** 隐藏页面中某个元素的几种方法

- display: none

  - 元素不会显示出来,不会占用任何空间

- visibility: hidden

  - 元素虽然不可见,但是会占用元素该有的空间

- rgba()

  - 通过设置透明度,不会影响后代元素(会占用空间)

- opacity: 0~1

  - 0 是完全透明
  - 影响该元素的所有后代元素(会占用空间)

- 绝对定位于当前页面的不可见位置

  ```css
  position: absolute;
  top: -9000px;
  left: -9000px;
  ```





## 12. box-sizing有什么作用？content-box和border-box的区别

**box-sizing是用来设置盒子宽高的行为(就是设置标椎盒模型和IE盒模型)**

- content-box: 所设置的宽高是:  内容 -- 标椎盒模型
  - 设置padding和border会将盒子撑大
- border-box:  所设置的宽高是: 内容+padding+margin -- IE盒模型
  - 设置padding和border不会将盒子撑大





## 13. 为什么会发生样式抖动

* 因为没有指定元素具体高度和宽度,比如数据还没有加载进来时元素高度是 100px(假设这里是100px) 
* 数据加载进来后,因为有了数据,然后元素被大,所有出现了抖动





## 14. 说说浮动常见的规则？

* 元素浮动后,脱离标准流
* 浮动只能左右浮动, 不能超出包含块的左右边界
* 浮动元素之间不能**层叠**
  * 如果⼀个元素浮动，另⼀个浮动元素已经在那个位置了，后浮动的元素将紧贴着前⼀个浮动元素
  * 如果水平方向剩余的空间不够显示浮动元素，浮动元素将向下移动，直到有充足的空间为止
* 浮动元素不能用与行内级内容层叠,行内级内容会被浮动元素推出
  - 图文环绕效果





## 15. 为什么需要清除浮动？清除浮动有几种方法？

* 因为浮动元素脱离了标准流,想要在浮动元素后面添加标准流元素,得不到想要的效果

* 三种方法

  - 给父元素设置固定高度(不推荐)
  - 在父元素后面增加一个空的块级子元素,并设置clear:both(不推荐)
  - 给父元素添加一个伪元素

  ```js
  .clear_fix::after {
      content: "";
      clear: both;
      display: block;
      /* 浏览器兼容 */
      visibility: hidden;
      height: 0;
  }
  /* 兼容IE6/7 */
  .clear_fix {
  	*zoom: 1;
  }
  ```

  





## 16. 伪类与伪元素有什么区别?

* 伪类使用单冒号 伪元素使用双冒号
  * :hover -- 伪类
  * ::before -- 伪元素
* 伪元素会在文档流生成⼀个新的元素，并且可以使用 content  属性设置内容





## 17. 结构伪类nth-child(n)和nth-of-type(n)的区别？

* nth-child(n)
  * 选中父元素的第几个子元素 , 计数时与元素的类型无关。
* nth-of-type(n)
  * 与nth-child(n)类似 只会计算符合同种类型的元素





## 18. 元素水平垂直居中的方案

#### 水平居中

###### 1, 行内级元素

设置父元素的text-align : center

###### 2, 块级元素

设置当前块级元素(前提是这个块级元素要有宽度) margin : 0 auto;

###### 3, flex布局

justify-content: center

###### 4, 相对定位:left/translate(行内元素无效)

position: relative;

left: 50%; // 百分比是相对于包含块

transform: translate(-50%, 0); // 百分比是相对于自身

**translate只针对块级和行内块级元素,行内元素不会生效**

###### 5, 绝对定位:元素有宽度的情况下

width: 100px(必须)

left: 0

right: 0

margin: 0 auto

###### 6, 绝对定位:left/margin-left(不能用百分比)

width: 100px(必须)

left: 50%;

margin-left: -50px; // margin-left的百分比是相对于包含块(父元素)的宽度



#### 垂直居中

###### 1, line-height(让文本垂直居中)

###### 2, flex布局

align-items: center

弊端 : flex布局中所有元素都会被垂直居中,相对来说兼容性差一点(基本可以忽略)

###### 3, 相对定位:top/translate(行内元素无效)

让元素向下位移父元素的50%

再让元素向上位移自身的50%

position: relative;

top: 50%;

transform: translate(0, -50%);

**translate只针对块级和行内块级元素,行内元素不会生效**

###### 4, 绝对定位

元素有高度的情况下

height: 100px(必须)

top: 0

bottom: 0

margin: auto 0

弊端 : 绝对定位脱离了标椎流,必须设置高度

###### 5, 绝对定位:top/margin-top

高度不能省略

height:100px(必须)

top:50%

margin-top: -50px





## 19. rem、em、vw、vh 单位是什么意思?

绝对单位: px

相对单位: rem、em、vw、vh

* em  理解为是相对于当前元素的font-size
  * 官网的叙述是 在 font-size 中使用是相对于父元素的字体大小
  * 这是因为font-size属性是可继承的
  * 当当前元素或父元素字体大小改变时,又需要重新计算了 层级较深时,会比较复杂,所以出现了rem
* rem  相对于的是HTML根元素的字体大小
  * CSS3新增的一个相对单位 r就是root的缩写 它的出现就是为了解决em的缺点
  * 任意浏览器的默认字体大小默认是16px 所以一般 1rem = 16px
* vw  视口宽度 根据窗口的宽度，分成100等份
* vh  视口高度 根据窗口的高度，分成100等份





## 20. 什么是视口(viewport)? 说说对视口的理解？

* pc端的视口

  * 就是浏览器的可视区域

* 移动端的视口

  * 布局视口

    * 会按照一个默认宽度980px,来布局一个页面盒子的内容
    * 为了可以显示完整的页面,会对整个页面进行缩小

    ```html
    <!-- width: 设置布局视口的宽度 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    ```

  * 视觉视口

    * 显示在可视区域的视口,就是视觉视口

  * 理想视口

    * 当布局视口 = 视觉视口的时候,就是理想视口
    * 怎样是这理想视口呢?

    ```html
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0">
    ```

    



## 21. 移动端适配的方案有哪些？

* 百分比布局
  
  * 因为不同属性百分比的值，相对的可能是不同的参照物，所以百分比很难统一
  
* rem +  动态HTML的 font-size (两个步骤)
  * **第一步：动态计算 HTML font-zise**
    
    - A. 用媒体查询来修改HTML font-size( 缺点不能实时改变font-size的大小 )
    - B. 自己编写JS来实现修改HTML font-size的大小(可以实时修改字体大小)
    
    ```js
    // 1.获取html元素
    const htmlEl = document.documentElement;
    
    function setRemUnit() {
      // 2.获取html的宽度(视口宽度)
      const htmlWidth = htmlEl.clientWidth;
      // 3.根据宽度计算一个和html的font-size的大小
      const HTMLFontSize = htmlWidth / 10;
      // 4.将font-size设置到html上
      htmlEl.style.fontSize = HTMLFontSize + "px";
    }
    // 保证第一次进来时, 可以设置一次font-size
    setRemUnit();
    
    // 当屏幕尺寸发生变化时, 实时来修改html的font-size
    window.addEventListener("resize", setRemUnit);
    ```
    
    - C. 是引用lib-flexiable库来实现（原理是JS动态改HTML font-size大小）
  
  * **第二步：px 转成rem**
    * 375设计稿 假设font-size的大小设置为当前屏幕的十分之一
      * 100px的盒子转rem -> `1rem=37.5px` `1px = 1/37.5rem` `100px = 100/37.5rem`
    * A. 手动计算 rem(不推荐)
    * B. Less的映射来计算(不推荐)
    * C. postcss-pxtorem插件来实现（webpack插件)
    * D. cssrem VSCode插件来实现 (px to rem)
  
* vw
  
  * **不需要**动态计算HTML font-zise
    * 假设375设计稿 font-size: 视口的宽度 / 10
    * 1vw 正好等于 视口宽度 / 100 
    * 所以 HTML font-zise = 10vw
  * px 转成 vw
    - A. 手动计算vw(不推荐)
    - A. Less的映射来计算(不推荐)
    - B. Postcss-px-to-viewport的插件(postcss插件)
    - C. cssrem VSCode插件
  
* flex弹性布局





## 22. 什么是Flexible Box布局？

* 弹性盒子是一种用于按行或按列布局元素的一维布局方法
* Flex 布局有两根轴线，分别为主轴和交叉轴。
  * 主轴由 flex-direction 定义，另⼀根轴垂直于它。







## 23. flex布局container 和 item的属性分别有哪些？以及其作用？

##### flex container中的属性

* **flex-direction** 决定主轴(main axis)的方向  ----row(默认值)、row-reverse、column、column-reverse
* **flex-wrap** 决定是单行还是多行  ----nowrap(默认):单行    wrap:多行
* **flex-flow** 是flex-direction和flex-warp的简写:  顺序任意,并且都可以省略
* **justify-content** 决定了 flex items 在 main axis(主轴) 上的对齐方式
* **align-items** 决定了 flex items 在 cross axis(交叉轴) 上的对齐方式
* **align-content** 决定了**多行** flex items 在 cross axis 上的对齐方式，用法与 justify-content 类似

##### flex item中的属性

* **flex-grow** 决定了 flex items 如何扩展(拉伸/成长)，默认值是 **0**
* **flex-shrink** 决定了 flex items 如何收缩(缩小)默认值是 **1**
* **flex-basis** 基础尺寸  具体的宽度数值(100px) , 默认值auto
* **flex** `none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ] | auto`
* **order** 决定了 flex items 的排布顺序 可以设置任意整数（正整数、负整数、0），值越小就越排在前面
* **align-self** 可以通过 align-self 覆盖 flex container 设置的 align-items





## 24. 常见的CSS Transform形变有哪些?

Transform形变

* 平移 : translate(x,y)
* 缩放 : scale(x,y)  /skeɪl/
* 旋转 : rotate(deg)
* 倾斜 : skew(deg,deg)  /skjuː/





## 25. 说说CSS Transition和Animation动画的区别

- transition
  - **transition是过度属性**，强调过度，它的实现需要触发一个事件（比如鼠标移动上去，焦点，点击等）才执行动画
  - 从一个位置移动到另一个位置,并在这个过程中加上一定的动画
  - transition只能定义开始状态和结束状态,不能定义之间状态,也即是说只有两个状态
  - transition不能\重复执行,除非再次触发动画
  - transition需要在特定状态下触发再会执行,比如某个属性被修改了(width从100px--->200px)
- animaiton
  - **animation是动画属性**，它的实现不需要触发事件，设定好时间之后可以自己执行，且可以循环一个动画。
  - animation 可以通过关键帧(keyframes)定义动画序列(每一帧怎样执行,也就是说可以设置多帧)





## 26. css 动画与 js 动画哪个性能更好

* CSS3 的动画:
  * 在性能上会稍微好⼀些，浏览器会对 CSS3 的动画做⼀些优化（比如专门新建⼀个图层⽤来跑动画） 　　 
  * 代码相对简单，但在动画控制上不够灵活 　　 
  * 兼容性不好 　　 
  * 部分动画功能⽆法实现（如滚动动画，视差滚动等）
* JS动画
  * 好弥补了css缺点，控制能力很强
  * 可以单帧的控制、变换，同时写得好完全可以兼容 IE6，并且功能强大
* 总结
  * 对于⼀些复杂控制的动画，使用 javascript 会比较好。而在实现⼀些小的交互动效的时候，可以多考虑 CSS 



## 26. 对requestAnimationframe的理解

* 实现动画效果的方法比较多 比如
  * Javascript 中可以通过定时器 setTimeout 来实现
  * CSS3 中可以使用 transition 和 animation 来实现
  * HTML5 中的 canvas 也可以实现
  * 除此之外，HTML5 提供一个专门用于请求动画的API，那就是 requestAnimationFrame **请求动画帧**
* window.requestAnimationFrame() 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行。
* **语法：** `window.requestAnimationFrame(callback);`  其中，callback是**下一次重绘之前更新动画帧所调用的函数**(即上面所说的回调函数)。该回调函数会被传入DOMHighResTimeStamp参数，它表示requestAnimationFrame() 开始去执行回调函数的时刻。该方法属于**宏任务**，所以会在执行完微任务之后再去执行
* **取消动画：** 使用cancelAnimationFrame()来取消执行动画，该方法接收一个参数——requestAnimationFrame默认返回的id，只需要传入这个id就可以取消动画了
* 优势
  * **CPU节能**：使用SetTinterval 实现的动画，当页面被隐藏或最小化时，SetTinterval 仍然在后台执行动画任务，由于此时页面处于不可见或不可用状态，刷新动画是没有意义的，完全是浪费CPU资源。而**RequestAnimationFrame**则完全不同，当页面处理未激活的状态下，该页面的屏幕刷新任务也会被系统暂停，因此跟着系统走的RequestAnimationFrame也会停止渲染，当页面被激活时，动画就从上次停留的地方继续执行，有效节省了CPU开销
  * **函数节流**：在高频率事件( resize, scroll 等)中，为了防止在一个刷新间隔内发生多次函数执行，RequestAnimationFrame可保证每个刷新间隔内，函数只被执行一次，这样既能保证流畅性，也能更好的节省函数执行的开销
  * **减少DOM操作**：requestAnimationFrame 会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成
* setTimeout执行动画的缺点
  * 它通过设定间隔时间来不断改变图像位置，达到动画效果。但是容易出现卡顿、抖动的现象；原因是
    * settimeout任务被放入异步队列，只有当主线程任务执行完后才会执行队列中的任务，因此实际执行时间总是比设定时间要晚
    * settimeout的固定时间间隔不一定与屏幕刷新间隔时间相同，会引起丢帧



## 27. 说说vertical-align的作用以及应用场景？

* vertical-align会影响**行内块级元素**在一个**行盒**中垂直方向的位置
* vertical-align默认值是baseline : 默认是基线对齐
  - 基线
    - 文本的基线是字母x的下方
    - Inline-block默认的baseline是margin-bottom的底部（没有，就是盒子的底部）
    - Inline-block有文本时，baseline是最后一行文本的x的下方
* top : 把行内级盒子的顶部跟line boxes(**行盒**)顶部对齐
* middle：行内级盒子的中心点与父盒基线加上x-height一半的线对齐 
* bottom：把行内级盒子的底部跟line box底部对齐 





## 28. 说说你对BFC的理解

* B**FC就是用来决定块级盒子是如何排布的**

* 要知道BFC首先要知道FC的概念 : formatting context 格式化上下文 ,页面上所有的内容都是格式化上下文的一部分
* BFC :  block formatting context  块级格式化上下文
  * 是页面的一块渲染区域 并且有一套渲染规则,决定了子元素如何定位 以及与其他元素之间的排列 布局之间的关系
  * BFC是一个独立的布局环境 相当于是一个容器 在其中按照一定的规则对块级元素进行摆放 ,并且不会影响其他的布局环境中的盒子,如果一个元素触发BFC则BFC中的元素布局不受外界的影响
* 块级元素在标椎流里面都是在BFC中布局的---->这是因为根元素<html>会创建BFC
* 创建BFC的条件
  - 根元素（<html>）
  - float left/right
  - position absolute/fixed
  - overflow: 除visible
  - display: inline-block等
* 特点
  - 在BFC中,box会在垂直方向上一个挨着一个的排布
  - 垂直方向的间距由margin属性决定
  - 在**同一个BFC中**，相邻两个box之间的margin会折叠
  - 在BFC中，每个元素的左边缘是紧挨着包含块的左边缘的
* 作用
  - 可以利用BFC处理margin的折叠问题,浮动的高度塌陷问题

##### MDN上有整理出在哪些具体的情况下会创建BFC

- 根元素（<html>） 
- 浮动元素（元素的 float 不是 none） 
- 绝对定位元素（元素的 position 为 absolute 或 fixed） 
- 行内块元素（元素的 display 为 inline-block） 
- 表格单元格（元素的 display 为 table-cell，HTML表格单元格默认为该值），表格标题（元素的 display 为 table-caption，HTML表格标题默认为该值） 
- 匿名表格单元格元素（元素的 display 为 table、table-row、 table-row-group、table-header-group、table-footer-group（分别是HTML table、 row、tbody、thead、tfoot 的默认属性）或 inline-table） 
- overflow 计算值(Computed)不为 visible 的块元素 
- 弹性元素（display 为 flex 或 inline-flex 元素的直接子元素） 
- 网格元素（display 为 grid 或 inline-grid 元素的直接子元素） 
- display 值为 flow-root 的元素 

##### BFC官方文档解读

- 在BFC中,box会在垂直方向上一个挨着一个的排布
- 垂直方向的间距由margin属性决定
- 在**同一个BFC中**，相邻两个box之间的margin会折叠
- 在BFC中，每个元素的左边缘是紧挨着包含块的左边缘的

##### BFC的应用 - 消除折叠效果

* 在**同一个BFC中**，相邻两个box之间的margin会折叠
* 给某一个元素放到另外一个BFC中

##### BFC的应用 - 浮动高度塌陷

* 网上有很多说法，BFC可以解决浮动高度塌陷，可以实现清除浮动的效果,他们也压根没有办法解释，为什么可以解决浮动高度的塌陷问题，但是不能解决绝对定位元素的高度塌陷问题呢？ 
* 使用BFC解决高度塌陷问题,需要满足两个条件
  1. 浮动元素的**父元素**触发BFC,形成独立的BFC(的块级格式化上下文)
  2. 浮动元素的**父元素**的高度是auto
* 解决浮动元素高度塌陷问题是源于一个盒子是BFC时，它高度的计算规则
  * 当一个盒子是BFC且高度设置为auto时，它会在计算高度时要求增加高度以包裹浮动元素的下边缘
  * 那么为了包裹浮动元素的下边缘增加了高度，就不会出现高度塌陷问题了
  * 绝对定位元素(absolutely positioned box)   **会被忽略**   **ignore**





## 29. 介绍下 BFC、IFC、GFC 和 FFC

* BFC（Block formatting contexts）：块级格式上下文
* IFC（Inline formatting contexts）：内联格式上下文
* GFC（GrideLayout formatting contexts）：网格布局格式化上下文
* FFC（Flex formatting contexts）:⾃适应格式上下⽂





## 30. 说出不同像素之间的差异？

分为三种像素:设备像素(物理像素),设备独立像素(逻辑像素),css像素

* 设备像素(物理像素)
  - 是指显示器上真实的像素,在购买显示器或者手机的时候，提到的设备**分辨率**就是设备像素的大小
  - iPhone X的分辨率 1125 x 2436，指的就是设备像素
* 设备独立像素(逻辑像素)
  - 如果面向开发者我们使用设备像素显示一个100px的宽度，那么在不同屏幕上显示效果会是不同的
  - 开发者针对不同的屏幕很难进行较好的适配，编写程序必须了解用户的分辨率来进行开发
  - 所以在设备像素之上，操作系统为开发者进行抽象，提供了设备独立像素的概念
  - 比如你购买了一台显示器，在操作系统上是以1920x1080设置的显示分辨率，那么无论你购买的是2k、4k的显示器，对于开发者来说，都是1920x1080的大小
  - 如果设备像素很大的时候,比如2k,4k等,可以理解为一个设备独立像素里面由多个设备像素来渲染的
* css像素
  - 默认情况下就是设备独立像素(也就是逻辑像素)





## 31. 分析比较 opacity: 0、visibility: hidden、display: none 优劣和适用场景

结构

* display:none: 会让元素完全从渲染树中消失，渲染的时候不占据任何空间, 不能点击
* visibility:hidden:不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，不能点击
* opacity:0: 不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，可以点击

继承

* display: none和opacity: 0：是非继承属性
* visibility: hidden：是继承属性性
  * 子孙节点消失由于继承了hidden，通过设置visibility: visible;可以让子孙节点显式

性能

* display:none : 修改元素会造成⽂档回流,读屏器不会读取display: none元素内容，性能消耗较大
* visibility:hidden: 修改元素只会造成本元素的重绘,性能消耗较少读屏器读取visibility: hidden元素内容
* opacity: 0 ： 修改元素会造成重绘，性能消耗较少

联系

* 它们都能让元素不可⻅





## 32. 如何解决移动端 Retina 屏 1px 像素问题





## 33. 如何用 css 实现多行文本溢出省略效果？并考虑兼容性？

单行

```css
text-overflow:ellipsis; 规定当文本溢出时，显示省略符号来代表被修剪的文本
overflow: hidden; 文字长度超出限定宽度，则隐藏超出的内容
white-space: nowrap; 设置文字在一行显示，不能换行
```

多行

```css
overflow: hidden;
text-overflow: ellipsis;
-webkit-line-clamp: 2; //行数
display: -webkit-box;
-webkit-box-orient: vertical;
```

* -webkit-line-clamp: 2：
  * 用来限制在一个块元素显示的文本的行数，为了实现该效果，它需要组合其他的WebKit属性）
* display: -webkit-box：和1结合使用，将对象作为弹性伸缩盒子模型显示
* -webkit-box-orient: vertical：和1结合使用 ，设置或检索伸缩盒对象的子元素的排列方式





## 34. 如何计算白屏时间和首屏加载时间

白屏时间: 

* window.performance.timing.domLoading - window.performance.timing.navigationStart 

首屏时间: 

* window.performance.timing.domInteractive - window.performace.timing.navigationStart





## 35. 如何自定义滚动条的样式

滚动条相关样式都是伪元素，以 scrollbar 打头，有以下伪元素，从 -webkit 中可⻅兼容性⼀般， 

不过⽆所谓，现在 Chrome 浏览器占⼤头 

* ::-webkit-scrollbar — 整个滚动条. 

* ::-webkit-scrollbar-button — 滚动条上的按钮 (上下箭头). 

* ::-webkit-scrollbar-thumb — 滚动条上的滚动滑块. 

* ::-webkit-scrollbar-track — 滚动条轨道. 

* ::-webkit-scrollbar-track-piece — 滚动条没有滑块的轨道部分. 

* ::-webkit-scrollbar-corner — 当同时有垂直滚动条和⽔平滚动条时交汇的部分. 

* ::-webkit-resizer — 某些元素的 corner 部分的部分样式(例:textarea 的可拖动按钮).

但其实最常⽤的是以下⼏个伪元素：**滚动条、滑块、轨道**，如下滚动条设置成功

```css
::-webkit-scrollbar {
 width: 6px;
 height: 6px;
}
::-webkit-scrollbar-track {
 border-radius: 3px;
 background: rgba(0, 0, 0);
 box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.08);
}
::-webkit-scrollbar-thumb {
 border-radius: 3px;
 background: rgba(0, 0, 1);
 box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.2);
}
```



## 36. CSS3新增了那些特性？HTML5新增了那些特性?

* 一，选择器

  * :nth-child(n)
  * :nth-of-type(n)
  * ...

* 二，新样式

  * border-radius：创建圆角边框

  * box-shadow：为元素添加阴影
  * border-image：使用图片来绘制边框
  * 新增了新的颜色表示方式`rgba`与`hsla`
  * `text-shadow`可向文本应用阴影
  * ...

* 三，transition过度

* 四，transform转换

* 五，animation动画

* 六，渐变

  * linear-gradient





## 37. 什么是响应式设计？响应式设计的基本原理是什么？如何做？

##### 什么是响应式网站

* 响应式网站设计是一种网络页面设计布局，页面的设计与开发应当根据用户行为以及设备环境(系统平台、屏幕尺寸、屏幕定向等)进行相应的响应和调整
* 响应式网站常见特点：
  * 同时适配PC + 平板 + 手机等
  * 标签导航在接近手持终端设备时改变为经典的抽屉式导航
  * 网站的布局会根据视口来调整模块的大小和位置

##### 基本原理

* 响应式设计的基本原理是通过媒体查询检测不同的设备屏幕尺寸做处理，为了处理移动端，页面头部必须有`meta`声明`viewport`

  ```html
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no”>
  ```

##### 响应式方案

* 媒体查询
* 百分比
  * 比如当浏览器的宽度或者高度发生变化时，通过百分比单位，可以使得浏览器中的组件的宽和高随着浏览器的变化而变化，从而实现响应式的效果
* vw/vh
* rem





## 38. 如果要做优化，CSS提高性能的方法有哪些？

* 内联首屏关键CSS

  * 在打开一个页面，页面首要内容出现在屏幕的时间影响着用户的体验，而通过内联`css`关键代码能够使浏览器在下载完`html`后就能立刻渲染
  * 而如果外部引用`css`代码，在解析`html`结构过程中遇到外部`css`文件，才会开始下载`css`代码，再渲染
  * 所以，`CSS`内联使用使渲染时间提前
  * 注意：但是较大的`css`代码并不合适内联（初始拥塞窗口、没有缓存），而其余代码则采取外部引用方式

* 异步加载CSS

  * 

* 资源压缩

  * 利用`webpack`、`gulp/grunt`、`rollup`等模块化工具，将`css`代码进行压缩，使文件变小，大大降低了浏览器的加载时间
  * css单一样式: `margin-top` 会比 `margin`的执行效率
  * 减少使用@import, 它是等待页面加载完成之后再进行加载. 建议使用link, 它是在页面加载时一起加载的

* 合理使用选择器

  * 如果嵌套的层级更多，页面中的元素更多，那么匹配所要花费的时间代价自然更高

    所以我们在编写选择器的时候，可以遵循以下规则：

    - 不要嵌套使用过多复杂选择器，最好不要三层以上
    - 使用id选择器就没必要再进行嵌套
    - 通配符`*{}`和属性选择器效率最低，避免使用

* 减少使用昂贵的属性

  * 在页面发生重绘的时候，昂贵属性如`box-shadow`/`border-radius`/`filter`/透明度/`:nth-child`等，会降低浏览器的渲染性能

* 其他

  * 慎重使用高性能属性：浮动、定位
  * 尽量减少页面重排、重绘
  * 去除空规则：｛｝。空规则的产生原因一般来说是为了预留样式。去除这些空规则无疑能减少css文档体积
  * cssSprite，合成所有icon图片，用宽高加上backgroud-position的背景图方式显现出我们要的icon图，减少了http请求
  * 把小的icon图片转成base64编码
  * ...





## 39. 让Chrome支持小于12px 的文字方式有哪些？区别？

Chrome 中文版浏览器会默认设定页面的最小字号是12px，英文版没有限制

原由 Chrome 团队认为汉字小于12px就会增加识别难度





## 40. 说说对CSS预编语言的理解？有哪些区别?

预处理语言 扩充了 `Css` 语言，增加了诸如变量、混合（mixin）、函数等功能，让 `Css` 更易维护、方便

本质上，预处理是`Css`的超集

三大优秀的预编处理器:

* sass

  ```js
  2007 年诞生，最早也是最成熟的 Css预处理器
  文件后缀名为.sass与.scss，可以严格按照 sass 的缩进方式省去大括号和分号
  ```

* less

  ```js
  2009年出现，受SASS的影响较大，但又使用 Css 的语法，让大部分开发者和设计师更容易上手
  缺点是比起 SASS来，可编程功能不够，不过优点是简单和兼容 Css，反过来也影响了 SASS演变到了Scss 的时代
  ```

* stylus

  ```js
  2010 年产生，来自 Node.js社区，主要用来给 Node 项目进行 Css 预处理支持
  ```

  

##### 基本使用

* less和scss

  ```less
  .box {
    display: block;
  }
  ```

* sass

  ```Sass
  .box
    display: block
  ```

* stylus

  ```stylus
  .box
    display: block
  ```



##### 嵌套

三者的嵌套语法都是一致的，甚至连引用父级选择器的标记 & 也相同

```less
.a {
  &.b {
    color: red;
  }
  &:hover {}
}
```



##### 变量

* less

  ```less
  @red: #c00;
  
  strong {
    color: @red;
  }
  ```

* sass声明的变量跟less十分的相似，只是变量名前面使用`$`开头



##### 作用域



##### 混入

混入（mixin）应该说是预处理器最精髓的功能之一了，简单点来说，`Mixins`可以将一部分样式抽出，作为单独定义的模块，被很多选择器重复使用

* less

  ```less
  .nowrap_ellipsis {
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
  }
  .box1{
    width: 300px;
    height: 100px;
    background-color: pink;
    .nowrap_ellipsis();
  }
  ```



##### 代码模块化

模块化就是将`Css`代码分成一个个模块

`scss`、`less`、`stylus`三者的使用方法都如下所示

```less
@import './common';
@import './reset';
```



## 41. 什么是1px问题，如何去解决，如何画出0.5px边框？

在移动端的设计搞中，UI给的设计稿往往是750px，图中边框宽度为1px，在375px的设备下，我们的宽度因为0.5px

但是直接设置成0.5的话，一些设备或者浏览器并不支持0.5px

方案一： viewport + rem + dev（淘宝）

方案二：伪元素 + transform（京东）

```html
<div class="test">满300-50</div>
.test::before{
	content: "";
	position: absolute;
	left: 0;
	top: 0;
    height:200%;
    width:200%;
	border: 1px solid red;
    transform: scale(0.5);
	transform-origin: 0 0;
}
```



## 42. 通常你会采取哪些措施来确保在不同的浏览器上的兼容性？

不同浏览器存在兼容性问题的核心原因是：不同的浏览器可能使用的时不同的浏览器内核

其实在现代工程化的开发架构下，大多数的浏览器兼容性问题是可以通过工程化中的配置选项来解决的

* 比如browserslist可以配置目标浏览器或者node环境，然后在不同的工具中起作用，比如autoprefixer/babel/postcss-preset-env等，在进行了正确的配置后，开发的Vue或者React项目在进行打包时，会自动根据目标环境来添加CSS前缀、Babel代码转换等。

* 如果想要额外的适配，通常会在项目中我们还会引入normal.css和polyfills来添加特定的CSS、JS的适配问题

* 还有一些事针对移动端的，比如移动端点击300ms的延迟、移动端1px边框的问题，都可以在特定的环境或者需求下来解决
* 当遇到问题时，很重要的事我们需要多查询caniuse的网站来确定某些特性的兼容性
* 另外如果针对特定的用户使用的事不同的浏览器和设备时，我们需要使用特定的工具，比如BrowserStack这样的工具来进行测试，遇到特定问题时，及时的解决和处理





## 43. 在 HTML 中，如何让一个图片自适应容器的大小？

* 使用 CSS 的`object-fit`属性，可以设置为`contain`（保持宽高比，完整显示图片）、`cover`（保持宽高比，完全覆盖容器）、`fill`（拉伸图片填充容器）等。

* 设置图片的`width`和`height`为 100%。

```css
img{
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```





























































