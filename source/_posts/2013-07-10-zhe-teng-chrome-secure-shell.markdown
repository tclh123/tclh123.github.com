---
layout: post
title: "折腾Chrome Secure Shell"
date: 2013-07-10 01:23
comments: true
categories: Chrome,OS X,SSH
---

> 最近的觉悟是自己写代码太慢，对IDE的依赖是累积的，各种恶性循环（不足够了解语言，不熟悉项目结构）。半天憋不出几行代码，这种状态让人厌恶...以前对此持观望态度，各种纵容自己，现在发现这已经成为自己的一大瓶颈...

这东西上次hack day的时候看[
atupal](https://github.com/atupal)用过，印象蛮深。今天挖出来玩玩。

去[商店](https://chrome.google.com/webstore/detail/secure-shell/pnhechapfaindjhompbnflcldabbghjo?utm_source=chrome-ntp-icon)安装的时候，提示`This application is not supported on this computer. Installation has been disabled. `，安装按钮直接变灰了。Google无果，看了下自己的Chrome版本，22...（mbp买来到现在没更过的节奏...），然后用"关于"里的自动更新报Error 12（以前也是这样所以一直没更吧..）。

##OS X下更新Chrome遇到Error 12

试了[官方](https://support.google.com/chrome/answer/1367288?hl=en)提供的方法，木有用。。Google出来的也大致都是删掉SoftwareUpdate然后再装一遍的意思，以及[各种偏方](http://www.v2ex.com/t/52249)，无果。

然后想是不是因为现在版本太低（22->28）的缘故，最后直接把最新的[下来](https://www.google.com/intl/en/chrome/browser/)覆盖了。后来发现完全无痛啊，因为现有的东西包括Extensions的localStorage都是放在`Application Support/`里的么。。

##配置Secure Shell

然后很舒服地用着最新版，顺利地把Secure Shell装上了。

然后其实也不用什么配置是吧，输个`<username>@localhost`就好了。。结果报Connection refused。。用iTerm试了下`ssh localhost`同样是Connection refused（sshd服务没开的节奏...）

``` bash 启动sshd服务
sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist # unload是停止服务
```

``` bash 查看是否启动
sudo launchctl list | grep ssh
...
-   0   com.openssh.sshd # 看到这个说明成功启动了
```

ok，现在已经可以顺利ssh到本地了。

另外，还可以直接授权publickey，这样就不用每次都输密码了（但是还是要输一次id_rsa私钥的密码，后面貌似shell会记住）。

``` bash 直接把id_rsa.pub写入authorized_keys文件就行了
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

##配置SSH root用户登陆

用自己的账户登陆是ok了，但是尝试用root登陆时提示`Permission denied (publickey,keyboard-interactive)`错误。

先是加了/etc/sshd_config里的`PermitRootLogin yes`（开始把ssh_config跟sshd_config搞错了。。图样）。还是不行。

后来发现是OS X默认没有开启root用户，我输入的密码也只是`a valid sudoer password`，根本不是root的密码。

``` bash 设置root的密码
sudo passwd
```

之后就可以用root账户登陆了。

##其他

Chrome Secure Shell 用起来很方便也很爽。但是我发现`ls`的时候中文目录名会乱码，中文文件内容可以正常显示。

还有就是不能输入中文（输入法无效。。）。

[http://git.chromium.org/gitweb/?p=chromiumos/platform/assets.git;a=tree;f=chromeapps/hterm](http://git.chromium.org/gitweb/?p=chromiumos/platform/assets.git;a=tree;f=chromeapps/hterm)，这个据说是前端的源码，可以拿来研究下（[kido](https://github.com/tclh123/kido)参考）。但是clone了半天搞不下来。。= =（噗。。现在看了一下貌似死在3%了..）

##Reference

- https://discussions.apple.com/thread/1141223?start=0&tstart=0
- http://blog.smitec.net/posts/setting-up-a-git-server-on-osx/
- http://superuser.com/questions/555810/how-do-i-ssh-login-into-my-mac-as-root

