---
layout: post
title: "Vim学习笔记（三）"
date: 2013-01-30 00:37
comments: true
categories: Vim
---

这次主要是一些跟窗口有关的操作。

##Vim窗口操作

---

###分割窗口
####1.打开已有文件

:split - 水平分，可以简写成 sp

:vsplit - 垂直分，可简写成 vs

####2.新建文件

:new+{name} - 水平新建窗口，name为文件名

:vnew+{name} - 垂直

###选择窗口

ctil+w {h|j|k|l} 上下左右切换窗口

##比较文件

---

:diffsplit {filename} - 对{filename}开一个新窗口，并比较。同vimdiff命令。

:diffpatch {patchfile} - 给当前buffer打上{patchfile}补丁后显示。

:diffthis - 使当前窗口加入diff。
