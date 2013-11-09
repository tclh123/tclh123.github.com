---
layout: post
title: "pip uninstall editable pkgs"
date: 2013-11-06 17:32
comments: true
categories: python, pip
---

http://stackoverflow.com/questions/17346619/how-to-uninstall-editable-packages-with-pip-installed-with-e

At {virtualenv}/lib/python2.7/site-packages/

- remove the egg file (e.g. distribute-0.6.34-py2.7.egg)
- from file easy_install.pth, remove the corresponding line (it should be a path to the source directory or of an egg file).

