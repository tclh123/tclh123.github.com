---
layout: post
title: "homebrew symlink error"
date: 2013-01-11 12:55
comments: true
categories: homebrew OSX
---

用homebrew的时候经常遇到symlinks出错，

``` bash
Linking /usr/local/Cellar/libpng/1.5.13... Warning: Could not link libpng. Unlinking...

Error: Could not symlink file: /usr/local/Cellar/libpng/1.5.13/share/man/man5/png.5
/usr/local/share/man/man5 is not writable. You should change its permissions.
```

需要修改目录拥有者，

``` bash
sudo chown -R `whoami` /usr/local/share/man/man5
```

