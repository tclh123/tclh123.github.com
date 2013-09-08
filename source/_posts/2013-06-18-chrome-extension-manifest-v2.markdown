---
layout: post
title: "Chrome Extension manifest V2"
date: 2013-06-18 01:28
comments: true
categories: Chrome Extension
---

今天兴起想写个 Chrome Extension，研究了一番，稍有点头绪。
想到天天用的 Fawave，去找了下它[源码](http://code.google.com/p/falang/source/checkout)（原项目名叫falang...好名字！）。

不看不知道，一看发现它逻辑这么复杂。。而且光看popup.html我就头大了。。
那个神一样模版语言（`<?js ... ?>...#{...}...`）。。见都没见过。

搞半天弄清楚他用的是[shotenjin.js](http://www.kuwata-lab.com/tenjin/jstenjin-users-guide.html)，是tenjin.js的子集，用于client-side。略小众啊，都搜不到什么相关信息。不过超轻量，整个就100多行代码，用法也真心简单。

又看了半天源码，似乎摸清楚几个困惑的点，

- chrome extension 的 popup.html 不支持持久化，每次点一下相当于要重新载入
- 像我这种比较小的需求，应该就是每次载入都从localStorage里拿数据出来更新DOM
- fawave那些timeline用localStorage肯定放不下的，貌似是利用 background.html 来做本地缓存（cache。写得好像很吊，就看了一点）。

总结一下，其实上面几个点就是纠结 popup.html 里的数据的持久化。

墨迹完了~~

##真正跟标题相关的内容

fawave用的是manifest V1，我用的V2。于是我用shotenjin.js来解析模版就出现了问题。

```
Uncaught Error: Code generation from strings disallowed for this context
```

经过一番搜索。。。发现是V2不再支持eval()，而shotenjin.js里必须用了eval()啊。。。

具体解决方法参照，

[Chrome extension 升级到 manifest version 2 的问题](http://www.360marks.com/?p=375)

[Using eval in Chrome Extensions. Safely.](http://developer.chrome.com/trunk/extensions/sandboxingEval.html)

因为不想换模版引擎，我用的是官方给的方法，用一个sandbox 的iframe，来代替进行eval()。。

但是。。仍然有问题（好吧这个问题证明是我是小白），简单说就是我想在popup.html load的时候就进行模版渲染，但是那个时候iframe里的script还没执行，message事件还没注册。。

解决方法是，

```
$('sandbox').onload = function() {
    init();
}
```

这样保证 init（给iframe发消息让它渲染模版）时， iframe 已经 load，就行了。

