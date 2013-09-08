---
layout: post
title: "Prolog语言"
date: 2013-05-02 17:11
comments: true
categories: prolog, Programming language
---

*Not Finished yet*

选了个人工智能的选修，教的是prolog（为啥不教lisp..）

prolog好老了，看了下介绍，貌似是种描述型语言，不带流程控制，依靠数据间的关系（逻辑），自动进行推理（所谓智能）。

##语言基本内容

###项

![](MyImage/prolog_1.png)

###语句

只有三种语句，事实、规则、问题（目标）。
语句都要用点(.)结束。

基本就是离散数学里的数理逻辑部分那个意思，前提、产生式、结论。

> Prolog语言是一种以一阶谓词为基础的逻辑性语言（Programming in logic）。

从命题逻辑，到谓词逻辑（加入谓词、量词）形成一阶逻辑系统。回想了下，数理逻辑好像很厉害的样子，不过学完了也记不得多少理论的东西了...

####事实

格式：P. （P表示一个谓词公式，即<谓词名>(<项表>)）
含义：无条件成立，恒为真
eg. like(monkey, banana)

####规则

格式：P :- P1, P2, ..., Pn. （:- 表示 蕴含，即->，,表示 合取/与，及^）
含义：若P1, ...,Pn均为真，P为真

####问题（目标）

格式：Q1,Q2,...Qm.
含义：待回答的问题，即Q1,...Qm同时为真吗？

###表


###谓词

##后续

Ps.由于课没去过几次，今天看ppt发现课上讲的是Turbo Prolog（呵呵..我说咋差这么大呢），[Wiki](http://en.wikipedia.org/wiki/Prolog#Related_languages)上说

> Visual Prolog, formerly known as PDC Prolog and Turbo Prolog, is a strongly typed object-oriented dialect of Prolog, which is very different from standard Prolog. As Turbo Prolog it was marketed by Borland, but it is now developed and marketed by the Danish firm PDC (Prolog Development Center) that originally produced it.

Prolog好几种方言啊，咱还是用GNU吧（找到个[for OS X的IDE](http://sourceforge.net/projects/xgp/)）。
