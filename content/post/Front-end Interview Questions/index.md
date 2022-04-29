---
title: "Front-end Interview Questions"
date: 2022-03-04T13:17:15+08:00
draft: true
lastmod: 
image: 
categories:
    - Notes
tags:
    - Programming
---

1. JavaScript 数据类型
   - 7种基本（原始）类型：string，Number，Bigint，Boolean，null，undefined，Symbol
   - Object
   
2. `stopPropagation` 和 `preventDefault` 的作用
   - `event.stopPropagation()` 方法防止调用相同事件的传播（向上冒泡到父元素或向下捕获到子元素，如嵌套 div 的点击事件）
   - `event.preventDefault()` 阻止事件的默认动作
   - `event.stopImmediatePropagation()` 彻底阻止其之后的绑定在元素上的其他监听事件
   
3. [`null` 与 `undefined`](https://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html)
   
4. `Symbol` 的使用场景
   
   - 消除魔法字符
   - 作为对象属性，防止有多个属性的复杂对象误覆盖某个属性名
   - 模拟类的私有方法
   
5. `for` 循环里的 `setTimeout`
   
   当同步和异步代码同时存在时，异步代码会在同步代码全部执行完成后再调用。

   ```javascript
   for (var i = 0; i < 10; i++){
     setTimeout((i) => {
       console.log(i);
     }, 0)
   }
   // setTimeout 会在指定时间后触发。如果同步代码执行时间（或者其他在它之前执行异步代码）大于设定时间，那么它将在其他代码执行完成后立即执行。
   ```
   
   在每次循环中将 `setTimeout` 里面的代码 `console.log(i)` 放入任务队列时 `i`的值都是不一样的，但 `var` 声明的变量作用于函数作用域。开始执行异步任务队列中的代码时，引擎会开始在当前的作用域中开始找变量 `i`，但是当前作用域中并没有对变量 `i` 进行定义。这个时候就会在创造该函数的作用域中寻找 `i`。创建该函数的作用域就是全局作用域，这个时候就找到了 `for `循环中的变量 `i`，这时的 `i` 是全局变量，并且值已经确定：`10`。
   
   解决方法有：
   
   ```javascript
   // IIFE：setTimeout 中的立即执行函数不会等待定时器到点后再执行，相当于 setTimeout 外的普通同步函数
   for (var i = 0; i< 10; i++){
     ((i)=>{
       setTimeout(() => {
         console.log(i)
       },1000);
     })(i)
   }
   ```
   
   ```javascript
   // let 形成块级作用域
   for (let i = 0; i< 10; i++){
     setTimeout(() => {
       console.log(i) 
     }, 1000);
   }
   ```


6. [微任务、宏任务与 Event-Loop](https://juejin.cn/post/6844903657264136200)

7. `var` 声明提升

   只有声明的变量会提升，初始化的不会。

8. [`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Using_promises)

9. [`npm install`安装机制](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/22)

10. [CSS 选择器](https://www.runoob.com/cssref/css-selectors.html) 与 [优先级](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Specificity)

11. 如何隐藏页面元素

   - CSS 的 `display: none;`
     - 不渲染该元素：不占据页面空间、不影响布局
     - 无法响应点击事件
     - 可通过 DOM API 获取（如更改为 `display: block;`）
   - CSS 的 `visibility: hidden;`
     - 渲染透明元素：占据页面空间、影响布局
     - 可通过 DOM API 获取（如更改为 `visibility: visible;`）
     - 其他实现方式：CSS `opacity: 0;`
   - HTML5 的 `hidden` 属性
     - 不渲染该元素：不占据页面空间、不影响布局、不会被读屏器读取
     - 使用情形：
       - 元素和页面状态不相关
       - 用以给其它元素重复使用、提供信息而非给用户使用
     - 对比 `display: none;`的优势：如果使用 `display: none;`，想要恢复显示时不好确定应该恢复成 `block` 还是`flex`
     - CSS `display` 属性将覆盖 HTML `hidden` 属性
   - `margin`、`border`、`padding`、`height`、`width` 置 `0`
     - 元素内子元素或内容应设置 `overflow:hidden`以隐藏子元素
   - CSS 的 `position: absolute` 移出可视区域
   - CSS 的 `clip-path: polygon(0px 0px,0px 0px,0px 0px,0px 0px);`
     - 占据页面空间、无法响应点击事件

12. [Debounce 与 Throttle](https://medium.com/@alexian853/debounce-throttle-%E9%82%A3%E4%BA%9B%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC%E6%87%89%E8%A9%B2%E8%A6%81%E7%9F%A5%E9%81%93%E7%9A%84%E5%B0%8F%E4%BA%8B-%E4%B8%80-76a73a8cbc39)

13. Vue 与 React 的区别：[1](https://zhuanlan.zhihu.com/p/100228073) [2](https://www.zhihu.com/question/309891718)

14. [如何理解单向数据流？](https://juejin.cn/post/7010952312902385671)

15. [`setState` 是同步的还是异步的？](https://juejin.cn/post/6996846391108567077)

    如果 `setState` 在 React 能够控制的范围被调用，它就是异步的。比如合成事件处理函数, 生命周期函数, 此时会进行批量更新, 也就是将状态合并后再进行 DOM 更新。

    如果 `setState` 在原生 JavaScript 控制的范围被调用，它就是同步的。比如原生事件处理函数中, 定时器回调函数中, Ajax 回调函数中, 此时 `setState` 被调用后会立即更新 DOM 。

16. [React 事件系统](https://juejin.cn/post/6955636911214067720)

17. [`setState 原理`](https://juejin.cn/post/6997601527162470407)

18. [React 16 新特性](https://www.jianshu.com/p/24ed0bc34c12)

19. [React 15 与 16 的生命周期](https://segmentfault.com/a/1190000039716570)

20. [Redux 原理](https://segmentfault.com/a/1190000023084074) 与 [复现](https://zhuanlan.zhihu.com/p/50247513)

21. [React Hook](https://juejin.cn/post/6844904165500518414)

22. [TCP协议](https://hit-alibaba.github.io/interview/basic/network/TCP.html)、[TCP 与 UDP 协议的区别](https://www.cnblogs.com/fundebug/p/differences-of-tcp-and-udp.html)

23. 三次握手与四次握手

    ![img](https://s2.loli.net/2022/03/13/qs6MbPDr8hta7ez.jpg)

24. [cookies](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)

25. 进程与线程

    线程是最小的执行单元，而进程由至少一个线程组成。如何调度进程和线程，完全由操作系统决定，程序自己不能决定什么时候执行，执行多长时间。     

26.   [HTML5 新特性](https://www.cnblogs.com/jane-panyiyun/p/13092297.html)

27.   [CSS 定位（Position）](https://www.runoob.com/css/css-positioning.html)

28.  [垂直水平居中的实现](https://liuyib.github.io/2020/04/07/css-h-and-v-center/)

     - 水平居中

       - 行内元素 `text-align: center`

       - 块级元素 `margin: 0 auto`

       - `position: absolute`  `left: 50%` `transform: translateX(-50%)`

       - `display: flex` `justify-content: center`

     - 垂直居中

       - 设置 `line-height` 等于 `height`

       - `position: absolute` `top: 50%` `transform: translateY(-50%)`

       - `display: flex` `align-items: center`

       - `display: table` `display: table-cell` `vertical-align: middle`

29.  [JavaScript 异步机制](https://juejin.cn/post/6844903556084924423)

30.  [ES6 新特性](https://www.jianshu.com/p/99c15f9bff27)

31.  [箭头函数特性](https://www.jianshu.com/p/e3af91d61102)

32.  [绑定事件的方式](https://juejin.cn/post/6844903720136736775)

33.  [React 组件间通信](https://segmentfault.com/a/1190000023585646)

34. [深拷贝与浅拷贝](https://juejin.cn/post/6844904197595332622)

35. [从 0 开始一个前端项目](https://segmentfault.com/a/1190000017158444)

36. [作用域链、闭包原理](https://segmentfault.com/a/1190000039745946) 与 [作用](https://segmentfault.com/a/1190000021725949)

37. [死锁](https://www.cnblogs.com/wkfvawl/p/11598647.html)

38. [HTTP 与 HTTPS](https://zhuanlan.zhihu.com/p/72616216)

39. [HTTP 2.0](https://runnerliu.github.io/2020/10/25/tcpdiff/)

40. [原型链](https://segmentfault.com/a/1190000021232132)

41. 继承方式及优缺点

    **原型链继承的缺点：**字面量重写原型会中断关系，使用引用类型的原型，并且子类型还无法给超类型传递参数。

    **借用构造函数（类式继承）：**借用构造函数虽然解决了刚才两种问题，但没有原型，则复用无从谈起。

    **组合式继承：**思路是使用原型链实现对原型属性和方法的继承，而通过借用构造函数来实现对实例属性的继承。既通过在原型上定义方法实现了函数复用，又保证每个实例都有它自己的属性。

42. [事件代理 / 事件委托](https://www.cnblogs.com/liugang-vip/p/5616484.html)

43. 从输入 URL 到展示页面的全过程 [1](https://shawnzhou.world/2021/05/30/the-URL-from-the-input-to-the-page-display-process/) [2](https://segmentfault.com/a/1190000006879700)

44. 页面渲染 HTML 的过程

    1. 浏览器解析 HTML 源码，然后创建一个 DOM 树。并行请求 CSS / Image / JS 在 DOM 树中，每一个 HTML 标签都有一个对应的节点，并且每一个文本也都会有一个对应的文本节点。DOM 树的根节点就是 `documentElement`，对应的是 `html` 标签。

    2. 浏览器解析 CSS 代码，计算出最终的样式数据。构建 CSSOM 树。对 CSS 代码中非法的语法它会直接忽略掉。解析 CSS 的时候会按照如下顺序来定义优先级：浏览器默认设置 < 用户设置 < 外链样式 < 内联样式 < HTML 中的 `style`。

    3. DOM Tree + CSSOM -> 渲染树。渲染树和 DOM 树有点像，但是是有区别的。DOM树完全和html标签一一对应，但是渲染树会忽略掉不需要渲染的元素，比如 `head`、`display:none` 的元素等。而且一大段文本中的每一个行在渲染树中都是独立的一个节点。渲染树中的每一个节点都存储有对应的 CSS 属性。

    4.一旦渲染树创建好了，浏览器就可以根据渲染树直接把页面绘制到屏幕上。

    以上四个步骤并不是一次性顺序完成的。如果 DOM 或者 CSSOM 被修改，以上过程会被重复执行。实际上，CSS 和 JavaScript 往往会多次修改 DOM 或者 CSSOM。

45. 怎样添加、移除、移动、复制、创建和查找节点？

    1. 创建新节点
       - `createDocumentFragment()`  创建一个DOM片段
       - `createElement_x()`  创建一个具体的元素
       - `createTextNode()`  创建一个文本节点

    2. 添加、移除、替换、插入
       - `appendChild()`
       - `removeChild()`
       - `replaceChild()`
       - `insertBefore()`

    3. 查找
       - `getElement**s**ByTagName()`  通过标签名称
       - `getElementsByName()`  通过元素的Name属性的值
       - `getElementById()`  通过元素Id，唯一性

46. [CSS 长度单位](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Values_and_units#%E9%95%BF%E5%BA%A6)

47. [CSS 盒子模型](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)

48. [块级格式化上下文 BFC 与清除浮动](https://segmentfault.com/a/1190000022626284)

     - 触发条件
        - 根元素
        - `float` 的值不是 `none`
        - `position` 的值不是 `static` 或者 `relative`
        - `display` 的值是 `inline-block`、`inline-flex`、`flex`、`flow-root`、`table-caption`、`table-cell`
        - `overflow` 的值不是 `visible`
     - 渲染规则
        - 内部的 Box 会在垂直方向，从顶部开始一个接一个地放置
        - Box 垂直方向的距离由 `margin` 决定。属于同一个 BFC 的两个相邻 Box 的 `margin` 会发生叠加
        - 每个元素的 margin box 的左边，与包含块 border box 的左边相接触(对于从左往右的格式化，否则相反)，即使存在浮动也是如此
        - BFC 的区域不会与 float box 叠加
        - BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之亦然
        - 计算 BFC 的高度时，浮动元素也参与计算

49.  `b` 与 `strong` 的区别：`b` 是实体标签，用来给文字加粗；而 `strong` 是逻辑标签，作用是加强字符语气；为了符合 CSS3 的规范，应尽量用 `strong`

50.  `img` 中的 `alt` 与 `title` 属性：`alt` 属性是在你的图片因为某种原因不能加载时在页面显示的提示信息，会直接输出在原本加载图片的地方；`title` 属性是在你鼠标悬停在该图片上时显示一个小提示

51.  [HTML 结构语义化](https://www.jianshu.com/p/6bc1fc059b51)

52.  [响应式设计](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/CSS_layout/Responsive_Design)

53.  CSS 关系选择器
    
    - 所有后代(包括所有隔代)  `p span { … }`
    - 直接后代(子元素)  `div>span { … }`
    - 后面的所有兄弟  `div~span { … }`
    - 后面的相邻兄弟  `div+p { … }`

54.  CSS 特性选择器
    
    ```css
    div[class] { … } /* 设置了class属性的div元素 */ 
    div[class="light"] { … } /* 设置light类的div元素 */
    ```
    
    - `~=abc`：包含值 `abc`（多个用空格分开的值）
    - `|=abc`：以 `abc-` 开头
    - `^=abc`：以` abc` 开头
    - `$=abc` ：以 `abc` 结尾
    - `*=abc` ：包含 `abc`
    
55.  [CSS 伪类选择器与伪元素选择器](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)

    - 伪类选择器
        - 不同状态：`a:link, visited, hover, facus, active`
        - 第一（最后一）个子元素：`td:first-child, last-child`
        - 唯一的 `p` 子元素：`p:only-child`
        - (倒数)第 n 个子元素：`nth-child(n), nth-last-child(n)`
        - 没有子元素的 `p` 元素：`p:empty`
        - 排除这些元素：`:not(selector)`
    - 伪元素选择器
        - 元素的一部分：`p::first-line, first-letter`
        - 前面或后面添加内容(content)：`p::before, after`（常用于插入一个提示性而不被读屏器读取的图标）
        - 被用户选取的元素部分：`::selection`

56.  CSS 选择器优先级计算

    - ID选择器的特殊性值，加 0,1,0,0。
    - 类选择器、属性选择器或伪类，加 0,0,1,0。
    - 元素和伪元素，加 0,0,0,1。
    - 通配选择器\*对特殊性没有贡献，即 0,0,0,0。
    - 最后比较特殊的一个标志!important（权重），它没有特殊性值，但它的优先级是最高的，为了方便记忆，可以认为它的特殊性值为 1,0,0,0,0。

57.  [经典排序算法详解](https://zhuanlan.zhihu.com/p/57088609)与[对比](https://www.runoob.com/w3cnote/ten-sorting-algorithm.html)

58. [`for` 与 `forEach` 的区别](https://mp.weixin.qq.com/s/aPFCrPGBTus_Spf1QL1WWA)

59. [二叉树、平衡二叉树、B树、B+树](https://zhuanlan.zhihu.com/p/27700617)

60. [红黑树](https://www.jianshu.com/p/e136ec79235c)

61. [树的应用场景](https://blog.csdn.net/qq_41475067/article/details/112794476)

62. [跳表](https://www.jianshu.com/p/9d8296562806)

63. [LSM 树](https://blog.csdn.net/jinking01/article/details/105377370)

64. [为什么数据库的索引使用 B+ 树](https://segmentfault.com/a/1190000023402876)

65. [浏览器的同源策略](https://developer.mozilla.org/zh-CN/docs/Web/Security/Same-origin_policy)

66. [JSONP](https://www.runoob.com/json/json-jsonp.html)

67. [图片懒加载](https://juejin.cn/post/6961227083573886984)

68. [XSS 与 CSRF](https://segmentfault.com/a/1190000007059639)

69. [React Hooks](https://blog.csdn.net/Charissa2017/article/details/106730493)

70. [Class 的静态方法定义](https://blog.csdn.net/qq_30100043/article/details/53542966)

71. [二叉树的深度优先搜索与广度优先搜索](https://www.cnblogs.com/goloving/p/14522449.html)

72. [重排、重绘](https://juejin.cn/post/6844904083212468238) 与 [优化](https://segmentfault.com/a/1190000039679970)

73. [类继承](https://zh.javascript.info/class-inheritance)

74. [原生 JS 实现 ajax 请求](https://juejin.cn/post/6844903764403421197)

75. [HTTP 状态码](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status)

76. [HTTP Heders](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers)

77. [Node 与 Element，`children` 与 `childNodes` 的区别](https://zhuanlan.zhihu.com/p/38813601)

78. 遍历 DOM 树 [1](https://zh.javascript.info/dom-navigation) [2](https://blog.csdn.net/qq_42853241/article/details/91406106) [3](https://www.cnblogs.com/tracylin/p/5220867.html) [4](https://segmentfault.com/a/1190000009112326)

## References

- [ES6 Symbol 使用场景](https://juejin.cn/post/6844903812046520328)
- [三种隐藏 HTML 元素的方式](https://www.jianshu.com/p/99d9fcde91cb)
- [[隐藏页面元素 css](https://www.cnblogs.com/houxianzhou/p/14610364.html)](https://www.cnblogs.com/houxianzhou/p/14610364.html)
- [页面渲染html的过程](https://www.cnblogs.com/georgexu/p/14047199.html)
- [css优先级计算规则](https://www.cnblogs.com/wangmeijian/p/4207433.html)

## Others' Notes

- [前端知识整理](https://hsip.me/fed/)
- [前端学习大汇总](https://chenhaoact.gitbooks.io/chenhaoact-fe-learn/content/)