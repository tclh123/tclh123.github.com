---
layout: post
title: "Vim学习笔记（一）"
date: 2013-01-06 19:40
comments: true
categories: Vim
---

从今天开始再好好学下Vim吧，其实也没这么难上手，多用用就好了。
先跟[这个tutorial](http://www.openvim.com/tutorial.html)学下。

##模式

---

Vim有Insert mode跟Command mode，按i进入insert mode，按ESC进入command mode。

##光标移动（Movement）

---

####上下左右（Basic movement）

hjkl。

####字移动（Word movement）

w - next word

e - end of the word

b - beginning of the word
####重复移动（Number powered movement）

3w - same as w 3 times

##重复插入

---

在command mode下先输入次数n，然后进入insert mode，正常插入一组字符，然后按ESC就会自动重复n-1组字符。