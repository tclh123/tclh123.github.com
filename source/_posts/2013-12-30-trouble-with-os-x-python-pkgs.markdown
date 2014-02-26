---
layout: post
title: "Trouble with OS X python pkgs"
date: 2013-12-30 12:26
comments: true
categories: python, OS X
---

## 起因

安装 https://github.com/amolenaar/gaphor 的时候总报 `ImportError: No module named pygtk`,
而我的 pygtk 是 homebrew 装的，

```
$ brew info pygtk
pygtk: stable 2.24.0
http://www.pygtk.org/
/usr/local/Cellar/pygtk/2.24.0 (658 files, 18M) *
  Built from source
From: https://github.com/Homebrew/homebrew/commits/master/Library/Formula/pygtk.rb
==> Dependencies
Build: pkg-config ✔
Required: glib ✔, gtk+ ✔, atk ✔, pygobject ✔, py2cairo ✔
==> Options
--glade
    Python bindigs for glade. (to `import gtk.glade`)
--universal
    Build a universal binary
==> Caveats
For non-homebrew python (2.x), you need to amend your PYTHONPATH like so:
  export PYTHONPATH=/usr/local/lib/python2.7/site-packages:$PYTHONPATH
```

（出问题后看pygtk有几个依赖是叉，还重装过一次）

`python -c "import pygtk"` 是 ok 的。

```
$ echo $PYTHONPATH
/usr/local/lib/python2.7/site-packages:

$ python -c "import sys, pprint; pprint.pprint(sys.path)"
['',
 '/Library/Python/2.7/site-packages/MySQL_python-1.2.3-py2.7-macosx-10.8-intel.egg',
 '/Library/Python/2.7/site-packages/pip-1.1-py2.7.egg',
 '/Library/Python/2.7/site-packages/distribute-0.6.49-py2.7.egg',
 '/Users/tclh123/Programming/douban/PyDoubanFM/src/douban-client',
 '/usr/local/lib/python2.7/site-packages',
 '/Users/tclh123/Dev/UML_Tools/gaphor-gaphor-0.17.2',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python27.zip',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/plat-darwin',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/plat-mac',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/plat-mac/lib-scriptpackages',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/lib-tk',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/lib-old',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/lib-dynload',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/PyObjC',
 '/Library/Python/2.7/site-packages',
 '/Library/Python/2.7/site-packages/setuptools-0.6c11-py2.7.egg-info',
 '/usr/local/lib/python2.7/site-packages/gtk-2.0']

```

`sys.path`中是包含 '/usr/local/lib/python2.7/site-packages' 的，homebrew 装的 pygtk 在这里面。

但是在 `cd gaphor-gaphor-0.17.2 && pip install .` 的时候，输出 `sys.path`

```
['/private/tmp/pip-RS454x-build/setuptools_git-1.0-py2.7.egg',
 '/private/tmp/pip-RS454x-build/nose-1.3.0-py2.7.egg',
 '.',
 '',
 '/Library/Python/2.7/site-packages/MySQL_python-1.2.3-py2.7-macosx-10.8-intel.egg',
 '/Library/Python/2.7/site-packages/pip-1.1-py2.7.egg',
 '/Library/Python/2.7/site-packages/distribute-0.6.49-py2.7.egg',
 '/Users/tclh123/Programming/douban/PyDoubanFM/src/douban-client',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python27.zip',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/plat-darwin',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/plat-mac',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/plat-mac/lib-scriptpackages',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/lib-tk',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/lib-old',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/lib-dynload',
 '/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/PyObjC',
 '/Library/Python/2.7/site-packages',
 '/Library/Python/2.7/site-packages/setuptools-0.6c11-py2.7.egg-info']
```

却不包含 '/usr/local/lib/python2.7/site-packages' 了。。为何

https://github.com/Homebrew/homebrew/issues/10908
这个 issue 是关于 Meld 的，依然没发现什么有帮助的信息么..

## python 在 OS X 下的 site-packages 目录

在我机子上分散在下列地方，

```
/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/  # 这个应该是系统自带python默认的地方?
/Library/Python/2.7/site-packages/  # 大部分pip装的似乎都到这里了
/usr/local/lib/python2.7/site-packages/  # homebrew 装的地方
```


问题还没搞清楚
**To be continued**


## easy_install on OS X

还有，我搞不清楚现在我 easy_install 装的东西是否 work 了，以及装的地方在哪里？

http://lukehagan.com/journal/2010-11-21-easy_install/

似乎依然不 work 迷茫中
