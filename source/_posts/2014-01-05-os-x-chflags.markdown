---
layout: post
title: "OS X chflags"
date: 2014-01-05 00:43
comments: true
categories: OS X, FreeBSD
---

U盘插过机房的机子后被某Windows上的2b病毒影响了，所有文件都被隐藏然后生成对应的 .lnk 的文件（Windows快捷方式）。
今天插OS X上一看，在图形界面下还是被隐藏的（说明文件/FAT32在OS X上挂载后，文件的隐藏属性跟Windows上的都可以上层兼容?）

OS X 实际上是 FreeBSD，Linux上隐藏文件/文件夹都只有取名为`.`开头的方法，BSD上还有 `chflags` 这个命令

```
CHFLAGS(1)                BSD General Commands Manual               CHFLAGS(1)

NAME
     chflags -- change file flags

SYNOPSIS
     chflags [-fhv] [-R [-H | -L | -P]] flags file ...

     ...

     The flags are specified as an octal number or a comma separated list of keywords.  The following keywords are currently defined:

           arch, archived
                   set the archived flag (super-user only)

           opaque  set the opaque flag (owner or super-user only).  [Directory is opaque when viewed through a union mount]

           nodump  set the nodump flag (owner or super-user only)

           sappnd, sappend
                   set the system append-only flag (super-user only)

           schg, schange, simmutable
                   set the system immutable flag (super-user only)

           uappnd, uappend
                   set the user append-only flag (owner or super-user only)

           uchg, uchange, uimmutable
                   set the user immutable flag (owner or super-user only)

           hidden  set the hidden flag [Hide item from GUI]
```

flag 前面加 `no` 就是相反的意思,
所以,

```
chflags nohidden *
```

就行了.
