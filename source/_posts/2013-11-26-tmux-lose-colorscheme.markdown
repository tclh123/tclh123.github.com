---
layout: post
title: "tmux lose colorscheme"
date: 2013-11-26 11:19
comments: true
categories: tmux, vim
---

```
alias tmux="TERM=screen-256color-bce tmux"
```

And set up the default-terminal option in `~/.tmux.conf`,

```
set -g default-terminal "screen-256color"
# set -g default-terminal "xterm"
```

## Reference

- http://rhnh.net/2011/08/20/vim-and-tmux-on-osx
- http://stackoverflow.com/questions/10158508/lose-vim-colorscheme-in-tmux-mode#comment24005530_10264470
- http://blog.longwin.com.tw/2011/04/tmux-learn-screen-config-2011/
