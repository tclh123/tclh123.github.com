---
layout: post
title: "Sublime Text 2 使用中文路径"
date: 2013-05-08 17:07
comments: true
categories: 
---

文件是中文路径的话，使用build system不能正常工作。

解决方法：

在OS X上，

```
subl /Applications/Sublime\ Text\ 2.app/Contents/MacOS/sublime_plugin.py
```

在文件末尾添加两行代码，

```
reload(sys) 
sys.setdefaultencoding('utf-8')
```
