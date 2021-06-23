---
title: 爬虫之Fiddler-Mono代理工具
date: 2019-05-22 23:12:35
tags: [Note, Spider]
categories: Note
---

近期做知网爬虫项目的一些工具准备 具体参见[Cyrus Ren blog](https://cyrusrenty.github.io//2018/12/19/cnkispider-1/)

## Fiddler介绍

> http调试代理工具，以代理服务器的方式监听系统的http网络数据流动

*mac下需要使用.Net编译后的程序，无法直接安装fiddler，故使用Mono Framework

## Mono Framework介绍

> **Mono**是一个由[Xamarin](https://zh.wikipedia.org/wiki/Xamarin)公司（先前是[Novell](https://zh.wikipedia.org/wiki/Novell)，最早为[Ximian](https://zh.wikipedia.org/wiki/Ximian)）所主持的自由开放源码项目。该项目的目标是创建一系列匹配[ECMA](https://zh.wikipedia.org/wiki/Ecma国际)标准（[Ecma-334](http://www.ecma-international.org/publications/standards/Ecma-334.htm)和[Ecma-335](http://www.ecma-international.org/publications/standards/Ecma-335.htm)）的[.NET](https://zh.wikipedia.org/wiki/.NET)工具，包括[C#](https://zh.wikipedia.org/wiki/C_Sharp)编译器和[通用语言架构](https://zh.wikipedia.org/wiki/通用语言架构)。与微软的[.NET Framework](https://zh.wikipedia.org/wiki/.NET_Framework)（[共通语言运行平台](https://zh.wikipedia.org/wiki/Common_Language_Runtime)）不同，Mono项目不仅可以运行于[Windows](https://zh.wikipedia.org/wiki/Windows)系统上，还可以运行于[Linux](https://zh.wikipedia.org/wiki/Linux)，[FreeBSD](https://zh.wikipedia.org/wiki/FreeBSD)，[Unix](https://zh.wikipedia.org/wiki/Unix)，[OS X](https://zh.wikipedia.org/wiki/OS_X)和[Solaris](https://zh.wikipedia.org/wiki/Solaris)，甚至一些游戏平台，例如：Playstation 3，Wii或XBox 360。(来自维基百科）

## Mac下安装 参见[简书陈康stozen](https://www.jianshu.com/p/57ec761cb5a3)

**1.Mono**

> 下载并安装：[http://www.mono-project.com/download/#download-mac](http://www.mono-project.com/download/#download-mac)

*从Mozilla LXR上下载所有受信任的root证书，存于Mono的证书库里。root证书能用于请求SSL地址。*

```
/Library/Frameworks/Mono.framework/Versions/<mono version>/bin/mozroots --import --sync
```

**2.修改配置文件**

如果想要运行Fiddler，还需要把Mono加入到环境变量中。编辑.bash_profile文件：

```
sudo vi ~/.bash_profile
```

添加下方文本：[注意查看本机下mono版本号]

```
export MONO_HOME=/Library/Frameworks/Mono.framework/Versions/5.0.1
export PATH=$PATH:$MONO_HOME/bin
```

存后重新打开Terminal，Mono环境已装好。

**3.Fiddler**

从Fiddler官网[https://www.telerik.com/download/fiddler](https://link.jianshu.com/?t=https://www.telerik.com/download/fiddler)下载**fiddler-mac.zip**的压缩包。解压到非中文字符的路径下。

运行：

```
sudo mono Fiddler.exe
```

mono版本不支持，则运行：

```
 sudo mono --arch=32 Fiddler.exe
```

界面显示：

**更多关于mac下使用fiddler 请见[Jerry Qu blog](https://imququ.com/post/use-fiddler-on-macos.html)**

