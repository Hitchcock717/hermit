---
title: HTML之DOM节点树
date: 2019-11-15 17:33:56
tags: [Note, Markdown]
categories: Note
---

 具体参见[菜鸟教程](https://www.runoob.com/htmldom/htmldom-tutorial.html)

## DOM概念

>DOM (Document Object Model) 译为**文档对象模型**，是 HTML 和 XML 文档的编程接口。
>
>HTML DOM 定义了访问和操作 HTML 文档的标准方法。
>
>DOM 以树结构表达 HTML 文档。

###*树形结构*

Document:

​			Root Document :<html>

​						Element:<head> 

​									Element:<title>

​												Text:"My title"

​						Element:<body>

​										Attribute:"href"

​										Element:<a>

​													Text:"My link"

​										Element:<h1>

​													 Text:"My header"

### *DOM Nodes*

```
<html>
  <head>
    <meta charset="utf-8">
    <title>DOM 教程</title>
  </head>
  <body>
    <h1>DOM 课程1</h1>
    <p>Hello world!</p>
  </body>
</html>
```

从上面的 HTML 中：

- <html> 节点没有父节点；它是根节点
- <head> 和 <body> 的父节点是 <html> 节点
- 文本节点 "Hello world!" 的父节点是 <p> 节点

并且：

- <html> 节点拥有两个子节点：<head> 和 <body>
- <head> 节点拥有两个子节点：<meta> 与 <title> 节点
- <title> 节点也拥有一个子节点：文本节点 "DOM 教程"
- <h1> 和 <p> 节点是同胞节点，同时也是 <body> 的子节点

并且：

- <head> 元素是 <html> 元素的首个子节点

- <body> 元素是 <html> 元素的最后一个子节点

- <h1> 元素是 <body> 元素的首个子节点

- <p> 元素是 <body> 元素的最后一个子节点

### *HTML DOM 方法*

getElementById() 方法返回带有指定 ID 的元素：

```
var element=document.getElementById("intro");
```

一些常用的 HTML DOM 方法：

- getElementById(id) - 获取带有指定 id 的节点（元素）
- appendChild(node) - 插入新的子节点（元素）
- removeChild(node) - 删除子节点（元素）

一些常用的 HTML DOM 属性：

- innerHTML - 节点（元素）的文本值
- parentNode - 节点（元素）的父节点
- childNodes - 节点（元素）的子节点
- attributes - 节点（元素）的属性节点



