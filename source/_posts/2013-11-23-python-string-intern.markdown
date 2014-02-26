---
layout: post
title: "python string intern"
date: 2013-11-23 19:44
comments: true
categories: python
---

今天在`__builtin__`里发现一个`intern`方法，（原来是internal的意思..
其实 C 里面有个文字常量区，就是说只要是字符串字面量都会存在那里。
才知道Python里不太一样，比如说
```
>>> a = 'a b'
>>> b = 'a b'
>>> a is b
False
```
真相是，python只对由`0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ_abcdefghijklmnopqrstuvwxyz`中的字符组成的字符串自动做intern。
因为它们可能会更短...更像标识符..
另外，在 Python 3 中，似乎被移到`sys.intern`中去了

##Reference

- http://stackoverflow.com/questions/1136826/what-does-python-sys-intern-do-and-when-should-it-be-used/1137293
