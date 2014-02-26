---
layout: post
title: "upgrade ack on ubuntu"
date: 2013-12-16 23:38
comments: true
categories: ack
---

```
mkdir ~/dpkgs
cd ~/dpkgs

wget http://packages.debian.org/sid/all/libfile-next-perl/download
wget http://packages.debian.org/sid/all/ack-grep/download
sudo dpkg -i libfile-next-perl_1.12-1_all.deb
sudo dpkg -i ack-grep_2.12-1_all.deb
```

## Reference

- http://stackoverflow.com/questions/7765813/ignoring-sub-directories-in-ackrc#answer-8012284
- http://askubuntu.com/questions/355668/how-to-install-ack-grep-2-0-with-apt-get
- http://askubuntu.com/questions/40779/how-to-install-a-deb-file-via-the-command-line
