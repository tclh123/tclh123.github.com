---
layout: post
title: "Core Java 2 读书笔记（一）"
date: 2013-05-13 22:51
comments: true
categories: 
---

我不会说我是因为明天考Java才开始看的。

鉴于记性实在太差，觉得以后每系统地学一个新的东西都要做一点笔记。。留给以后回忆用。。（“青春就是用来回忆的...”

从第三章开始看的，看到第六章。

##数据类型

- 基本类型，八种，int/short/long/byte，float/double，char，boolean
- 对象，都集成于Object类

ps. 没有unsigned类型，于是我就想...表示pixel的话，只能用-128~127的byte了...

##赋值与初始化

Java中只有声明（没有类似C/C++的定义一说，声明的同时可以初始化变量）。

##常量

用final修饰（const虽然为保留字，但目前还未定义）

## 操作符 ##

有一种`>>>`操作符，表示逻辑右移，`>>`是算术右移。

## 字符串equals ##

要使用`equals`来进行String的比较（覆盖了Object的equals），`==`只能判断两个串是否储存在同一位置。

## 格式化输出 ##

可以用`System.out.printf()`，类似C的printf。

*ps.不知道为什么书上介绍的是Format.printf()*

## 循环、分支 ##

`switch`语句的`case`标签必须是整数。

`break`还有一种带标签的break语句，用于跳出多层循环。

## 大数字 ##

BigInterger、BigDecimal，有add、subtract、multiply、divide、mod等方法。
用valueOf静态方法来转成大数字。

Java跟C++不同，程序员无法重载操作符。

## 数组 ##

`int[] a;`跟`int a[];`都可以用来声明数组。

`System.arraycopy(from, fromIndex, to, toIndex, count)`可以用来拷贝数组中的元素。

`Arrays.sort(a)`可以对数组排序。
*ps.开始我奇怪怎么没有类似的cmp函数，原来是在Comparable接口中定义了*

##Conclusion

四五六章后面几篇再写。。
