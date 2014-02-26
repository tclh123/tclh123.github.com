---
layout: post
title: "always trust .rvmrc file"
date: 2013-11-23 19:26
comments: true
categories: Ruby, .rvmrc
---

使用Octopress的时候目录里默认存在一个`.rvmrc`文件，
```
rvm use 1.9.3
```
目测是指定ruby版本用的。每次进入目录都会有`Do you wish to trust this .rvmrc file?`的提示，需要手动确认。
还是挺烦的...

其实，`rvm list` 可以看到我机子上只有这一个版本
```
rvm rubies

=> ruby-1.9.3-p327 [ x86_64 ]
```

所以这个 `.rvmrc` 是毫无意义的，可以删掉...
或者在`~/.rvmrc`里写入`export rvm_trust_rvmrcs_flag=1`
