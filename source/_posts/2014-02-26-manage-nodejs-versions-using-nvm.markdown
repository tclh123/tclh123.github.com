---
layout: post
title: "manage NodeJs versions using NVM"
date: 2014-02-26 23:08
comments: true
categories: nodejs, node, nvm
---

顾名思义啦，NVM(Node Version Manager).

根据 https://github.com/creationix/nvm 可以很方便地安装，

然后可以很方便地安装、管理各版本的node。

```
nvm install v0.10.26
```

装完后会显示 `Now using node v0.10.26`，而在新开的 shell 中需要 `nvm use v0.10.26`。所以设置一个默认版本，`nvm alias default v0.10.26`
貌似 nvm 只能管理使用 nvm 来安装的 nodes，然后按版本被安装到类似`$HOME/.nvm/v0.10.26`的 path.

安装 node 会附带安装 npm(Node Package Manager)。npm 安装 package 有两种模式，global 跟 local，local的概念就是只在项目目录下安装一份（其实js的安装也只是简单地拷贝文件嘛），这起到了类似 python venv 的功能，可以为每个项目单独隔离出一个包依赖环境。
那么，为了避免多次安装造成多次download，npm 默认会在 `$HOME/.npm` 目录下 cache 下载的包。`npm cache clean` 可以清空这个目录。

使用了 nvm 后， 附带的npm 被安装在了 `$HOME/.nvm/v0.10.26/lib/node_modules/npm/` （因为 npm 也只是一个 node module
而 global package 的安装目录变为 `$HOME/.nvm/v0.10.26/lib/node_modules`，bin 会被 symlink 到 `$HOME/.nvm/v0.10.26/bin`，它也已经被加入到 PATH 中.

```
npm config get prefix
```

另外，我原先的 node 都是用 homebrew 装的，

```
$ ls /usr/local/Cellar/node/
0.10.17 0.8.14
```

npm 被装在 /usr/local/lib/node_modules/npm -> /usr/local/Cellar/node/0.10.17/lib/node_modules/npm

npm prefix 为 /usr/local/share/npm，因而 npm global 包被装在 /usr/local/share/npm/lib/node_modules/
