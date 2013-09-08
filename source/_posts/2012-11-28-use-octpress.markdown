---
layout: post
title: "use octpress"
date: 2012-11-28 18:44
comments: true
categories: Octopress
---

繁杂的生活中让人更加萌生追求极简的欲望，心血来潮就打算那拿octopress再搭个博客（希望这个博客能够让我心宁静）。

*以下皆为回忆，可能由于某种原因记错，仅供参考...*
<!--more-->
但是这东西还真是超出我预期的让我折腾了很久，我的OSX默认是ruby是1.8的，octopress需要1.9.3，于是去安装rvm。

``` bash 安装rvm
curl -L https://get.rvm.io | sudo bash -s stable
```

装完还挺快的，接着就去装ruby 1.9.3，

``` bash
rvm install 1.9.3
```

然后直接跳出一个说明(vim)，说我gcc是lvvm-based的...不支持...要重装(= =!)，它提供了两个途径，然后我用brew装了gcc-4.2

``` bash 貌似是这样
brew install gcc-4.2
```

再去装ruby貌似就正常了，
等了半小时没反应...就根据[这篇](http://ruby-china.org/wiki/install_ruby_guide)用了[淘宝的镜像](http://ruby.taobao.org)，不过要注意OSX的[rvm路径不一样](http://blog.tclh123.com/165001)。然后速度就很快了...但是装到rubygem的时候，停在94%不动了...于是待机睡觉...
第二天看看还是停在94%...强制结束掉，然后重启reinstall，这次ok了。

然后，设置默认ruby版本为1.9.3

``` bash
rvm 1.9.3 --default
```

之后又折腾了几次octopress，主要是参考了以下几篇经验，

* http://voodeng.com/blog/2012/09/02/octopress-on-github/
* http://mrzhang.me/blog/blog-equals-github-plus-octopress.html

搞了几次，rake generate 有报错，参考[这篇](http://blog.visioncan.com/2012/octopress-rake-generate-error/)后，发现是我博文名字的问题，我取得是"Hello Octopress\!"...然后把`\!`删了就好了。
之后把博客绑定到了[oct.tclh123.com](http://oct.tclh123.com)上，

``` bash
echo 'oct.tclh123.com' >> source/CNAME
```

然后去DNS那加个oct到tclh123.github.com的CNAME。
至此，基本搞定。