---
title: "Basic Front-end Development Libraries"
date: 2022-02-21T20:38:19+08:00
draft: false
lastmod: 
image: "cover.webp"
categories:
    - Notes
tags:
    - Programming
    - Front-end Development Libraries
    - Bootstrap
    - React
    - Redux
    - freeCodeCamp
---

## Bootstrap：移动优先的响应性网页/应用程序前端框架

```html
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous"/> // 引入 Bootstrap

<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.8.1/css/all.css" integrity="sha384-50oBUHEmvpQ+1lW4y57PTFmhCaXp0ML5d60M1M7uH2+nqUivzIebhndOJK28anvf" crossorigin="anonymous"> // 引入 Font Awesome 图标库

<div class="container-fluid">
    <h2 class="text-primary text-center"></h2> // 主要文本、居中

    <img class="img-responsive" src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/running-cats.jpg"> // 图片自适应

    <button class="btn btn-default"></button> // Bootstrap 按钮

    <button class="btn btn-default btn-block"></button> // 块级元素（伸展并填满水平空间）

    <button class="btn btn-primary btn-block">Like</button> // 主题色，引导操作

    <button class="btn btn-info btn-block">Info</button> // 备选操作

    <button class="btn btn-block btn-danger">Delete</button> // 危险操作

    <div class="row"> // 12 列响应式栅格系统
    <div class="col-xs-4"><button class="btn btn-block btn-primary"><i class="fas fa-thumbs-up"></i> Like</button></div> // 点赞图标
    <div class="col-xs-4"><button class="btn btn-block btn-info"><i class="fas fa-info-circle"></i> Info</button></div>
    <div class="col-xs-4"><button class="btn btn-block btn-danger"><i class="fas fa-trash"></i> Delete</button></div>
  </div>

  // 通过使用行内元素 span 把不同的元素放在同一行，为一行的不同部分指定不同样式
  <p>Things cats <span class="text-danger">love</span></p>

  <form action="https://freecatphotoapp.com/submit-cat-photo">
    <div class="row">
      <div class="col-xs-6">
          <div class="well"></div> // 使页面更有层次感
          <label><input type="radio" name="indoor-outdoor"> Indoor</label>
      </div>
      <div class="col-xs-6">
        <label><input type="radio" name="indoor-outdoor"> Outdoor</label>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-4">
        <label><input type="checkbox" name="personality"> Loving</label>
      </div>
      <div class="col-xs-4">
        <label><input type="checkbox" name="personality"> Lazy</label>
      </div>
      <div class="col-xs-4">
        <label><input type="checkbox" name="personality"> Crazy</label>
      </div>
    </div>
    <input class="form-control" type="text" placeholder="cat photo URL" required> // 占满100%的宽度
    <button class="btn btn-primary" type="submit"><i class="fa fa-paper-plane"></i> Submit</button>
  </form>

</div>
```

## jQuery：用于简化HTML与JavaScript之间操作的跨浏览器 JavaScript 库

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.6.0.js"></script> // 引入

<script>
  $(document).ready(function() { // 防止代码在 HTML 页面呈现之前运行
    $("button").addClass("animated bounce"); // 所有的 jQuery 函数都以 $ 开头、添加跳跃效果类
    $(".well").addClass("animated shake");
    $("#target3").addClass("animated fadeOut");

    $("button").removeClass("btn-default"); // 移除类

    $("#target1").css("color", "blue"); // 改变 CSS

    $("button").prop("disabled", true); // 改变属性

    $("h3").html("<em>jQuery Playground</em>"); // 在标签里添加并替换原有 HTML 标签和文本

    $("#target4").remove(); // 移除元素

    $("#target4").appendTo("#left-well"); // 选取 HTML 标签并添加至另一个标签里

    $("#target2").clone().appendTo("#right-well"); // 复制标签

    $("#left-well").parent().css("background-color", "blue"); // 访问父标签

    $("#left-well").children().css("color", "blue"); // 访问子标签

    $(".target:nth-child(3)").addClass("animated bounce"); // 选取指定 class 或者元素类型的第 n 个标签

    $(".target:odd").addClass("animated shake"); // 奇偶（:even）选择器：jQuery 是零索引（zero-indexed）的，这意味着第 1 个标签的位置编号是 0。 :odd 表示选择第 2 个标签（位置编号 1），第 4 个标签（位置编号 3）……

    $("body").addClass("animated hinge"); // 掉落动画类

  });
</script>
```

## Sass：Syntactically Awesome StyleSheets，对 CSS 的扩展

```html
<style type='text/scss'>
  $text-color: red; // 允许使用变量
  .header{
    text-align: center;
  }
  .blog-post, h2 {
    color: $text-color;
  }

  nav { // 允许 CSS 嵌套
    background-color: red;
    ul {
        list-style: none;
        li {
        display: inline-block;
        }
    }
  }

  @mixin box-shadow($x, $y, $blur, $c){ // Mixins 创建可重用 CSS
    -webkit-box-shadow: $x $y $blur $c;
    -moz-box-shadow: $x $y $blur $c;
    -ms-box-shadow: $x $y $blur $c;
    box-shadow: $x $y $blur $c;
  }
  div {
    @include box-shadow(0px, 0px, 4px, #fff);
  }

  @mixin text-effect($val) { // 条件判断语句
    @if $val == danger {
        color: red;
    }
    @else if $val == alert {
        color: yellow;
    }
    @else if $val == success {
        color: green;
    }
    @else {
        color: black;
    }
  }

  @for $i from 1 through 12 { // @for 循环
    .col-#{$i} { width: 100%/12 * $i; } // #{$i} 将变量 i 与文本组合成字符串
  }
  // 相当于
  .col-1 {
    width: 8.33333%;
  }
  .col-2 {
    width: 16.66667%;
  }
  ...
  .col-12 {
    width: 100%;
  }

  @each $color in blue, red, green { // @each 循环遍历列表
    .#{$color}-text {color: $color;}
  }
  $colors: (color1: blue, color2: red, color3: green); // // @each 循环遍历映射
  @each $key, $color in $colors { // $key 变量引用 map 中的键
    .#{$color}-text {color: $color;}
  }
  // 相当于
  .blue-text {
    color: blue;
  }
  .red-text {
    color: red;
  }
  .green-text {
    color: green;
  }

  $x: 1; // @while 循环
  @while $x < 13 {
    .col-#{$x} { width: 100%/12 * $x;}
    $x: $x + 1;
  }

  // Partials：名称以下划线（_）字符开头，这样 Sass 就知道它是 CSS 的一小部分，而不会将其转换为 CSS 文件。 此外，Sass 文件以 .scss 文件扩展名结尾。例如，如果所有 mixins 都保存在名为 “_mixins.scss” 的 partial 中，并且在 “main.scss” 文件中需要它们
  @import 'mixins' // import 语句中不需要下划线

  .panel { // CSS 样式重用
    background-color: red;
    height: 70px;
    border: 2px solid green;
  }
  .big-panel {
    @extend .panel;
    width: 150px;
    font-size: 2em;
  }
</style>
```

## React：构建可重用组件驱动的用户界面

- JSX 是 JavaScript 的语法扩展，用以在 JavaScript 中编写 HTML
- 在花括号中编写希望被视为 JavaScript 的代码 `{ 'this is treated as JavaScript code' }`
- 转换器 Babel 将 JSX 编译成 JavaScript
- `ReactDOM.render(JSX, document.getElementById('root'))` 函数调用将 JSX 置于 React 自己的轻量级 DOM 中，React 使用自己的 DOM 快照来实现增量更新
- 嵌套的 JSX 必须返回单个元素，父元素包裹所有其他级别的嵌套元素

```javascript
const JSX = (
  <div className="myDiv"> // className 代替 class，属性和事件引用命名约定均变为驼峰式
    {/* 注释 */}
    <h1>Hello World</h1>
    <p>Lets render this to the DOM</p>
  </div>
  <div /> // 自闭合标签，无法在其中包含任何内容，用于渲染 React 组件
);
ReactDOM.render(JSX, document.getElementById('challenge-node')); // 渲染到 DOM 节点

const DemoComponent = function() { // JavaScript 函数创建无状态功能组件（能接收数据并对其进行渲染，但不管理或跟踪该数据的更改，不使用内部状态），是一个类，扩展了React.Component，返回 JSX 或 null，函数名以大写字母开头
  return (
    <div className='customClass' />
  );
};

class Kitten extends React.Component { // 扩展了 React.Component 的 ES6 类，可以访问 React 功能如本地状态和生命周期钩子
  constructor(props) {
    super(props); // 调用父类的构造函数（React.Component）
  }
  render() {
    return (
      <h1>Hi</h1>
    );
  }
}

const ChildComponent = () => { // App 父组件渲染子组件，组件可嵌套渲染
  return (
    <div>
      <p>I am the child</p>
    </div>
  );
};
class ParentComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>I am the parent</h1>
        <ChildComponent />
      </div>
    );
  }
};
ReactDOM.render(<ParentComponent />, document.getElementById('challenge-node')); // 渲染组件

const CurrentDate = (props) => {
  return (
    <div>
      <p>The current date is: {props.date}</p> // props 将属性传递给子组件
      // ES6 类组件则使用 {this.props.date} 访问
    </div>
  );
};
CurrentDate.defaultProps = { location: 'San Francisco' } // 设置默认 props
import PropTypes from 'prop-types';
MyComponent.propTypes = { location: PropTypes.func.isRequired } // 检查传入 props 的类型（func 代表 function，bool 代表 boolean）：https://reactjs.org/docs/typechecking-with-proptypes.html#proptypes
class Calendar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>What date is it?</h3>
        <CurrentDate date={Date()}/>
      </div>
    );
  }
};

// state 使用虚拟 DOM 来跟踪数据的变化，并根据数据的变化渲染 UI
// 当 state 数据更新时，它会使用该数据触发组件的重新渲染，包括接收 prop 数据的子组件
// React 只在必要的时候更新实际的 DOM。
class StatefulComponent extends React.Component { // 创建类组件必须扩展 React.Component
  constructor(props) {
    super(props);
    this.state = { // 通过在 constructor 中声明 state 属性在 React 组件中创建 state，属性为 object
      name: "John"
    }
    this.setState({ // 修改 State，React 可以异步批量处理多个 state 更新 👉 SHOULD NOT rely on their values for calculating the next state
      username: 'Lewis'
    });
    this.setState((state, props) => ({ // 以先前的状态和当前的属性设置状态的正确方法
      counter: state.counter + props.increment
    })); // object 应放在括号里以免被 JavaScript 认为代码片段
  }
  // render() 之前也可以从 state 或 props 中访问数据、对此数据执行计算等
  render() {
    return (
      <div>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};

class ControlledInput extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value // 访问传递的事件
    })
  }
  render() {
    return (
      <div>
        <input value={this.state.input} onChange={this.handleChange}></input>
        <h4>Controlled Input:</h4>
        <p>{this.state.input}</p>
      </div>
    );
  }
};
class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      submit: ''
    };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value // 访问传递的事件
    });
  }
  handleSubmit(event) {
    event.preventDefault(); // 防止新网页的默认的表单提交行为
    this.setState({
      submit: this.state.input
    });
  }
  render() {
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          <input value={this.state.input} onChange={this.handleChange}></input>
          <button type='submit'>Submit!</button>
        </form>
        <h1>{this.state.submit}</h1>
      </div>
    );
  }
}

// 生命周期方法：componentDidMount() shouldComponentUpdate() componentDidUpdate() componentWillUnmount()
// 应在将组件装载到 DOM 后被调用的 componentDidMount() 中对服务器进行 API 调用或任何其它调用，此处对 setState() 的任何调用都将触发组件的重新渲染，即在此方法中调用 API 并用 API​​ 返回的数据设置 state 时收到数据将自动触发更新；特定功能所需的任何事件监听器也应在其中添加
//  shouldComponentUpdate(nextProps, nextState) 返回一个 boolean，告诉 React 是否更新组件，防止组件接收到新的但没有改变的 props 时也重新渲染

<div style={{color: "yellow", fontSize: 16}}>Mellow Yellow</div> // 内联样式值为 object；属性名使用驼峰式；可以选择将字体大小设置为数字，省略单位 px，或者将其写为 "72px"

render() {
    // 修改这行下面的代码
    return (
       <div>
         <button onClick={this.toggleDisplay}>Toggle Display</button>
         {this.state.display && <h1>Displayed!</h1>} // 条件判断的简易写法：如果 condition 为 true，则返回标记；如果条件为 false ，则在评估 condition 后操作将立即返回 false，并且不返回任何内容
         // 也可使用三元运算符
       </div>
    );
  }

// ReactDOMServer.renderToString(<App />) 在服务器上渲染
// 当 React 应用程序最初加载到浏览器时包含一个代码量很少的 HTML 文件和一大堆 JavaScript，不利于搜索引擎索引
// 在服务器上渲染初始 HTML 标记并将其发送到客户端，则初始页面加载的内容包含搜索引擎可以抓取的所有页面标记
// React 仍然能够识别应用并在初始加载后进行管理。
```

## Redux：JavaScript 应用的可预测状态容器

Redux 中由且仅由一个状态对象负责应用程序的整个状态。

所有状态更新都由 dispatch action 触发，action 只是一个 JavaScript 对象，其中包含有关已发生的 action 事件的信息。Redux store 接收这些 action 对象，然后更新相应的状态。

```javascript
const LOGIN = 'LOGIN';
const LOGOUT = 'LOGOUT'; // 通常用常量消除魔法字符

const defaultState = {
  authenticated: false
};

const authReducer = (state = defaultState, action) => { // reducer 函数负责响应 action 进行状态的修改：以 state 和 action 作为参数，返回新的 state；reducer 不应该调用 API 接口、不应存在任何潜在的副作用
  switch (action.type) {
    case LOGIN: return { authenticated: true }
    case LOGOUT: return { authenticated: false }
    default: return state; // state 是只读的，永远不会直接修改状态，因此必须返回当前的 state；当程序有多个 reducer，每一个 action 被 dispatch 时它们都会运行，即使 action 与该 reducer 无关，此时要确保返回当前的 state
  }
};

const store = Redux.createStore(authReducer); // store 是一个保存和管理应用程序状态的 state

const loginUser = () => { // action creator
  return {
    type: LOGIN,
    message: "Hello!"
  }
};
const logoutUser = () => {
  return {
    type: LOGOUT
  }
};

store.dispatch(loginUser()); // 使用 dispatch 发送 action

let currentState = store.getState(); // 获取当前 state

let count = 0;
store.subscribe(() => count++); // 监听器函数只要 action 被 dispatch 就会被调用

const rootReducer = Redux.combineReducers({ // 组合多个 Reducers
  auth: authenticationReducer,
  notes: notesReducer
});

// Redux Thunk 中间件
// 判断每个经过它的action：如果是function类型，就调用这个function（并传入 dispatch 和 getState 及 extraArgument 为参数），而不是任由让它到达 reducer，因为到达 reducer 的 action 必须为 plain object
import thunkMiddleware from 'redux-thunk'
const REQUESTING_DATA = 'REQUESTING_DATA'
const RECEIVED_DATA = 'RECEIVED_DATA'
const requestingData = () => { return {type: REQUESTING_DATA} }
const receivedData = (data) => { return {type: RECEIVED_DATA, users: data.users} }
const handleAsync = () => {
  return function(dispatch) { // 以 dispatch 为参数，实现多次 dispatch
    dispatch(requestingData());
    setTimeout(function() {
      let data = {
        users: ['Jeff', 'William', 'Alice']
      };
      dispatch(receivedData(data));
    }, 2500);
  }
};
const defaultState = {
  fetching: false,
  users: []
};
const asyncDataReducer = (state = defaultState, action) => {
  switch(action.type) {
    case REQUESTING_DATA:
      return {
        fetching: true,
        users: []
      }
    case RECEIVED_DATA:
      return {
        fetching: false,
        users: action.users
      }
    default:
      return state;
  }
};
const store = createStore(asyncDataReducer, Redux.applyMiddleware(thunkMiddleware)) // 第二个参数引入中间件
```

**状态不变性关键原则**

 不可变状态意味着永远不直接修改状态，而是返回一个新的状态副本。

如果拍摄 Redux 应用程序一段时间状态的快照，会看到类似 `state 1，state 2，state 3，state 4，...` 等等，但每个状态都是一个独特的数据。这种不变性提供了时间旅行调试等功能。

但 Redux 并没有主动地在其 `store` 或者 `reducer` 中强制执行状态不变性（如状态中可变的 array 或 object）而需要手动实现。

object 状态可以使用 `Object.assign({}, obj1, obj2)` 拷贝对象实现状态不变性。

**React × Redux**

- 创建单一的 Redux store 来管理整个应用的状态（特定本地状态的独立组件除外）
- React 组件仅订阅 `store` 中与其角色相关的数据
- 直接从 React 组件中分发 `actions` 以触发 `store` 对象的更新

- `react-redux` 包提供 wrapper 组件 `Provider` 和 `connect`
- `Provider` 将 `state` 和 `dispatch` 作为组件的 `props`
    - `mapStateToProps()` 将 `state` 映射至对象上特定属性名上
    - `mapDispatchToProps()` 将 dispatch actions 映射到属性名上
    - `connect(mapStateToProps | null, mapDispatchToProps | null)(MyComponent)` 将参数中对象映射到 `props`
  
```javascript
// Redux:
const ADD = 'ADD';

const addMessage = (message) => {
  return {
    type: ADD,
    message: message
  }
};

const messageReducer = (state = [], action) => {
  switch (action.type) {
    case ADD:
      return [
        ...state,
        action.message
      ];
    default:
      return state;
  }
};

const store = Redux.createStore(messageReducer);

// React:
class Presentational extends React.Component { // Presentational 指未直接连接到 Redux 的 React 组件，只负责执行接收 props 的函数来实现 UI 的呈现
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    }
    this.handleChange = this.handleChange.bind(this);
    this.submitMessage = this.submitMessage.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  submitMessage() {
    this.props.submitNewMessage(this.state.input)
    this.setState((state) => ({
      input: ''
    }));
  }
  render() {
    return (
      <div>
        <h2>Type in a new Message:</h2>
        <input
          value={this.state.input}
          onChange={this.handleChange}/><br/>
        <button onClick={this.submitMessage}>Submit</button>
        <ul>
          {this.props.messages.map( (message, idx) => {
              return (
                 <li key={idx}>{message}</li>
              )
            })
          }
        </ul>
      </div>
    );
  }
};

// React-Redux:
const mapStateToProps = (state) => {
  return { messages: state }
};

const mapDispatchToProps = (dispatch) => {
  return {
    submitNewMessage: (newMessage) => {
       dispatch(addMessage(newMessage))
    }
  }
};

const Provider = ReactRedux.Provider;
const connect = ReactRedux.connect;

const Container = connect(mapStateToProps,mapDispatchToProps)(Presentational); // Container 组件用来连接到 Redux 上，负责把 actions 分派给 store、给子组件传入 store state 属性

class AppWrapper extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <Provider store={store}>
        <Container />
      </Provider>
    );
  }
};
```

**本地引入依赖**

```javascript
import React from 'react'
import ReactDOM from 'react-dom'
import { Provider, connect } from 'react-redux'
import { createStore, combineReducers, applyMiddleware } from 'redux'
import thunk from 'redux-thunk'

import rootReducer from './redux/reducers'
import App from './components/App'

const store = createStore(
  rootReducer,
  applyMiddleware(thunk)
);

ReactDOM.render(
  <Provider store={store}>
    <App/>
  </Provider>,
  document.getElementById('root')
);
```