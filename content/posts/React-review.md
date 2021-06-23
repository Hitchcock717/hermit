---
title: 前端之React语法
date: 2019-05-22 23:05:27
tags: [Note, React]
categories: Note
---
[具体参见菜鸟教程](https://www.runoob.com/react/react-install.html)

#### 腾讯云开发者平台+node.js环境+create-react-app脚手架

```
安装脚手架指令：sudo yarn global add create-react-app
```

关于yarn

> package dependence -从 npm 注册源获取模块的新的 CLI【command-line-interface】 客户端

```
创建app指令：create-react-app app
```

```
创建访问链接 cd app / yarn start ——> localhost+:本地端口3000
```

----

###*React元素渲染*

**将元素渲染进DOM(Document Object Model)文档对象模型**

```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8" />
<title>Hello React!</title>
<script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
<script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>
</head>
<body>

<div id="example"></div>     #首先定义根结点
<script type="text/babel">   #react第二代jsx语法解析编译器--babel
const element =<h1>Hello, world!</h1>;  #const表示常量，常量值不能通过重新赋值改变，不能重新声明 / 语法：const name1 = value1[, name2=value2 [, ..[, nameN=valueN]]]; / 此处标明元素是"Hello,world!"一级标题
ReactDOM.render( 						  #render()渲染方法，对一级标题渲染
    element,									#对应const中的元素 / 此处element可替换为<h1>Hello, world!</h1>
    document.getElementById('example') #返回匹配特定id的元素
);
</script>

</body>
</html>
```

**更新元素渲染**

```
<div id="example"></div>   
<script type="text/babel">
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>      #react中元素不可变
      <h2>现在是 {new Date().toLocaleTimeString()}.</h2>     #更新界面的唯一方法--创建新元素/ 此处创建计时器
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('example')
  );
}
 
setInterval(tick, 1000);    #setInterval()方法，每秒调用一次render()方法
```

**封装function tick( )**

```
等效方法一、
<div id="example"></div>
<script type="text/babel">
function Clock(props) {        #接受任意入参（props）
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>现在是 {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('example')
  );
}

setInterval(tick, 1000);

==================================================
等效方法二、
<div id="example"></div>
<script type="text/babel">
class Clock extends React.Component {    #使用ES6类
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>现在是 {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('example')
  );
}

setInterval(tick, 1000);
```

###### > 关于函数组件 参见[react官方文档](https://react.docschina.org/docs/components-and-props.html)

>如下可称为**函数组件**
>
>```
>function Welcome(props) {
>  return <h1>Hello, {props.name}</h1>;
>}
>```
>
>或
>
>```
>class Welcome extends React.Component {
>  render() {
>    return <h1>Hello, {this.props.name}</h1>;
>  }
>}
>```
>
>*渲染组件*
>
>React元素不仅包括DOM标签，还有用户自定义组件
>
>```
>function Welcome(props) {
>  return <h1>Hello, {props.name}</h1>;
>}
>
>const element = <Welcome name="Sara" />; #自定义Welcome name元素，注意与方法名一致【大写】
>ReactDOM.render(
>  element,
>  document.getElementById('root')
>);
>```
>
>让我们来回顾一下这个例子中发生了什么：
>
>1. 我们调用 `ReactDOM.render()` 函数，并传入 `<Welcome name="Sara" />` 作为参数。
>2. React 调用 `Welcome` 组件，并将 `{name: 'Sara'}` 作为 props 传入。
>3. `Welcome` 组件将 `<h1>Hello, Sara</h1>` 元素作为返回值。
>4. React DOM 将 DOM 高效地更新为 `<h1>Hello, Sara</h1>`。

​		*复合组件*

```
function Name(props) {
    return <h1>网站名称：{props.name}</h1>;
}
function Url(props) {
    return <h1>网站地址：{props.url}</h1>;
}
function Nickname(props) {
    return <h1>网站小名：{props.nickname}</h1>;
}
function App() {
    return (
    <div>
        <Name name="菜鸟教程" />
        <Url url="http://www.runoob.com" />
        <Nickname nickname="Runoob" />
    </div>
    );
}
 
ReactDOM.render(
     <App />,       #渲染整个组件
    document.getElementById('example')
);
```

###*React JSX*

>元素是构成 React 应用的最小单位，JSX 就是用来声明 React 当中的元素

**不能使用if else语句**——>**三元运算**

```
<div id="example"></div>
    <script type="text/babel">
	  var i = 1;
      ReactDOM.render(
      	<div>
      	  <h1>{i == 1 ? 'True!' : 'False'}</h1> #相当于 if i == 1, return true; else: return false;
        </div>
      	,
      	document.getElementById('example')
      );
```

######>关于三元运算

>语法：condition？expr1 ： expr2

**内联样式**

```
var myStyle = {
    fontSize: 100,
    color: '#FF0000'
};
ReactDOM.render(
    <h1 style = {myStyle}>菜鸟教程</h1>,
    document.getElementById('example')
);
```

**注释** {/*      */}

```
ReactDOM.render(
    <div>
    <h1>菜鸟教程</h1>
    {/*注释...*/}
     </div>,
    document.getElementById('example')
);
```

###*React State*  参见[胡子大哈blog]([http://huziketang.mangojuice.top/books/react/lesson10](http://huziketang.mangojuice.top/books/react/lesson10))

最直观的理解

![image_state](https://huzidaha.github.io/static/assets/img/posts/B7575C67-64F8-4A13-9C63-4D6805FA360D.png)

以点赞按钮为例

```
import React, { Component } from 'react'
import ReactDOM from 'react-dom'
import './index.css'

class LikeButton extends Component {
  constructor () {      
    super()
    this.state = { isLiked: false }  #this指向likebutton类
  }

  handleClickOnLikeButton () {
    this.setState({
      isLiked: !this.state.isLiked
    })
  }

  render () {
    return (
      <button onClick={this.handleClickOnLikeButton.bind(this)}>
        {this.state.isLiked ? '取消' : '点赞'} 👍
      </button>
    )
  }
}
```

######>关于constructor与super的作用    参见[掘金戴宏兵的文章](https://juejin.im/post/5b4c0b26f265da0f6c7a82a1)

`constructor` 方法是类的构造函数，是一个默认方法

`super` 这个关键字，既可以当做函数使用，也可以当做对象使用。这两种情况下，它的用法完全不用

​	当做函数使用

>**class** **A** {}
>**class** **B** **extends** **A** {
>**constructor**() {
>**super**();  // ES6 要求，子类的构造函数必须执行一次 super 函数，否则会报错。
>}
>}
>
>注：在 `constructor` 中必须调用 `super` 方法，因为子类没有自己的 `this` 对象，而是继承父类的 `this` 对象，然后对其进行加工,而 `super` 就代表了父类的构造函数。`super` 虽然代表了父类 A 的构造函数，但是返回的是子类 B 的实例，即 `super` 内部的 `this` 指的是 B，因此 `super()` 在这里相当于 ```A.prototype.constructor.call(this, props)``。

​	当做对象使用

**在普通方法中，指向父类的原型对象；在静态方法中，指向父类**

>class A {
>  c() {
>    return 2;
>  }
>}
>
>class B extends A {
>  constructor() {
>    super();
>    console.log(super.c()); // 2
>  }
>}
>
>let b = new B();
>
>注：上面代码中，子类 B 当中的 `super.c()`，就是将 `super` 当作一个对象使用。这时，`super` 在普通方法之中，指向 `A.prototype`，所以 `super.c()` 就相当于 `A.prototype.c()`。

**通过 super 调用父类的方法时，super 会绑定子类的 this**

```
class A {
  constructor {
    this.x = 1;
  }
  s() {
    console.log(this.x);
  }
}

class B extends A {
  constructor {
    super();
    this.x = 2;
  }
  m() {
    super.s();
  }
}

let b = new B();
b.m(); // 2

#上面代码中，super.s() 虽然调用的是 A.prototytpe.s()，但是 A.prototytpe.s()会绑定子类 B 的 this，导致输出的是 2，而不是 1。也就是说，实际上执行的是 super.s.call(this)。
```

######>继续state点赞👍案例

`isLiked` 存放在实例的 `state` 对象当中，这个对象在构造函数里面初始化。这个组件的 `render` 函数内，会根据组件的 `state` 的中的`isLiked`不同显示“取消”或“点赞”内容。并且给 `button` 加上了点击的事件监听。

最后构建一个 `Index` ，在它的 `render` 函数内使用 `LikeButton` 。然后把 `Index`渲染到页面上：

```
class Index extends Component {
  render () {
    return (
      <div>
        <LikeButton />
      </div>
    )
  }
}

ReactDOM.render(
  <Index />,
  document.getElementById('root')
)
```

### *React Props*

>state根据交互可变，用来更新和修改数据/props不可变，用来传递数据

```
<div id="example"></div>
<script type="text/babel">
function HelloMessage(props) {
	return <h1>Hello {props.name}!</h1>;
}

const element = <HelloMessage name="Runoob"/>; #自定义组件

ReactDOM.render(
	element,
	document.getElementById('example')
);
```

**state与props组合使用**

> 在父组件中设置 state， 并通过在子组件上使用 props 将其传递到子组件上。在 render 函数中, 我们设置 name 和 site 来获取父组件传递过来的数据。

```
class WebSite extends React.Component {
  constructor() {
      super();
 
      this.state = {
        name: "菜鸟教程",
        site: "https://www.runoob.com"
      }
    }
  render() {
    return (
      <div>
        <Name name={this.state.name} />
        <Link site={this.state.site} />
      </div>
    );
  }
}
 
 
 
class Name extends React.Component {
  render() {
    return (
      <h1>{this.props.name}</h1>
    );
  }
}
 
class Link extends React.Component {
  render() {
    return (
      <a href={this.props.site}>
        {this.props.site}
      </a>
    );
  }
}
 
ReactDOM.render(
  <WebSite />,
  document.getElementById('example')
);
```

