---
layout: post
title: "Vim学习笔记（四）- 插件篇"
date: 2013-01-30 01:02
comments: true
categories: Vim
---

主要是根据前辈的一篇博文，[谁说Vim不是IDE？（三）](http://www.cnblogs.com/chijianqiang/archive/2012/11/06/vim-3.html)写的，自己实践整理的一个记录。

下一步计划是消化这两篇：

1.[谁说Vim不是IDE？（四）](http://www.cnblogs.com/chijianqiang/archive/2012/12/17/vim-4.html)

2.[Maple's Vim config](https://github.com/humiaozuzu/dot-vimrc)

先是熟悉ctags，然后把vim搞成IDE，完善自己的.vimrc。

##pathogen

---

通过管理`runtimepath`来简化插件安装、运行时的文件，使其能位于自己自定义目录（默认为 bundle）下。

项目位于[github](https://github.com/tpope/vim-pathogen)

###插件安装

####1、执行

``` bash
mkdir -p ~/.vim/autoload ~/.vim/bundle; \
curl -Sso ~/.vim/autoload/pathogen.vim \
    https://raw.github.com/tpope/vim-pathogen/master/autoload/pathogen.vim
```

####2、在 .vimrc 中增加代码

``` vim
call pathogen#infect()
```

##Command-T

---

用于在一个给定目录下快速定位文件，Go To File的功能。

###插件安装

####1、下载

[command-t-1.4.vba](http://www.vim.org/scripts/download_script.php?src_id=18167)

####2、安装至bundle目录下

``` bash
mkdir ~/.vim/bundle/command-t
```

``` bash
vim command-t-1.4.vba
```
执行 `:UseVimball ~/.vim/bundle/command-t`

####3、编译C扩展

``` bash
cd ~/.vim/bundle/command-t/ruby/command-t
ruby extconf.rb
make
```

##Powerline

---

一个增强的窗口状态栏。

###插件安装

####1、安装到bundle

``` bash
cd ~/.vim/bundle
git clone git://github.com/Lokaltog/vim-powerline.git
```

####2、安装字体

安装一些 [vim-powerline patched fonts](https://gist.github.com/1595572)，我用的是Menlo，然后安装到系统

####3、在.vimrc中设置状态栏主题

```vim
"powerline{
"set guifont=PowerlineSymbols\ for\ Powerline
set guifont=Menlo\ for\ Powerline
set nocompatible
set t_Co=256
let g:Powerline_symbols = 'fancy'
"}
```