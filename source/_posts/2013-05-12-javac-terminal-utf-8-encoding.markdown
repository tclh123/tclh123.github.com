---
layout: post
title: "javac terminal utf-8 encoding"
date: 2013-05-12 19:38
comments: true
categories: OS X, java
---

OS X 的terminal输出信息是utf-8编码的，

但是javac默认输出GBK，会导致乱码。

可以用`javac -J-Dfile.encoding=UTF-8`来使其输出utf-8编码的信息。

解决方案:
```
echo "alias javac='javac -J-Dfile.encoding=UTF-8 '">>~/.bash_profile
```

###Reference

[解决javac和java命令在Mac OSX终端里的乱码问题](https://www.surfchen.org/archives/710)