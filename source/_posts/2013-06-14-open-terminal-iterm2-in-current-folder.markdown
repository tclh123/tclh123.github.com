---
layout: post
title: "Open Terminal(iTerm2) in Current Folder"
date: 2013-06-14 15:58
comments: true
categories: OS X, iTerm2
---

原来Terminal一直用自带的，现在改成iTerm2。
google到一些[用AppleScript解决的方案](http://www.dbform.com/html/2011/1559.html)，经测试不可用，估计是OS X 10.8改了什么东西。
没空研究AppleScript...

然后意识到也许可以把Go2Shell的默认Terminal改一下，然后确实google到了方法。。

##Solution

1. Download Go2Shell.
2. Change your default Go2Shell terminal to iTerm2.

``` bash
open -a Go2Shell --args config
```

That will open the configuration screen.


