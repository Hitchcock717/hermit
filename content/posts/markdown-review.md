---
title: 技术写作之Markdown
date: 2019-05-22 23:01:56
tags: [Note, Technical Writing]
categories: Note
---
标题

# #

## #

### #

#### #

###### #



引用 >

>

嵌套

> >
> >
> >> >
> >> >
> >> >>

区块内使用md语法

> # #
>
> 1. 有序列表
>
> * 无序列表 （*）

* 列表内使用引用

  >
  >
  >需要缩进

* [ ]   不勾选 [   ]

  

  

  代码 ```

  

  *斜体* * *

  **加粗** ** **

  

  [ 说明 ] ( http://xxxx.com ) 自动链接

  

  表格

  ```
  First Header | Second Header | Third Header
  :----------- | :-----------: | -----------:
  Left         | Center        | Right
  Left         | Center        | Right
  ```

  ```
  First Header | Second Header | Third Header
  ------------ | ------------- | ------------
  Content Cell | Content Cell  | Content Cell
  Content Cell | Content Cell  | Content Cell
  ```

  分割线

  ----

  

！图片[ 说明 ](/path/to/img.jpg)

流程图

```
​```graph
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->E;
    E-->F;
    D-->F;
    F-->G;
​```
```

时序图

```
​```graph
sequenceDiagram
    participant Alice
    participant Bob
    Alice->John: Hello John, how are you?
    loop Healthcheck
        John->John: Fight against hypochondria
    end
    Note right of John: Rational thoughts 
prevail...
    John-->Alice: Great!
    John->Bob: How about you?
    Bob-->John: Jolly good!
​```
```



甘特图

```
​```graph
gantt
        dateFormat  YYYY-MM-DD
        title Adding GANTT diagram functionality to mermaid
        section A section
        Completed task            :done,    des1, 2014-01-06,2014-01-08
        Active task               :active,  des2, 2014-01-09, 3d
        Future task               :         des3, after des2, 5d
        Future task2               :         des4, after des3, 5d
        section Critical tasks
        Completed task in the critical line :crit, done, 2014-01-06,24h
        Implement parser and jison          :crit, done, after des1, 2d
        Create tests for parser             :crit, active, 3d
        Future task in critical line        :crit, 5d
        Create tests for renderer           :2d
        Add to mermaid                      :1d
​```
```

