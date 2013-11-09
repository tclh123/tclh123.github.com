---
layout: post
title: "`python setup.py` install vs. `pip install .`"
date: 2013-11-08 00:28
comments: true
categories: python, pip
---

一些坑。

### Distutils
http://docs.python.org/2/distutils/setupscript.html#installing-package-data

### setuptools & pip

[Building and Distributing Packages with Setuptools](http://pythonhosted.org/setuptools/setuptools.html#using-find-packages)


https://pypi.python.org/pypi/setuptools/
http://www.pip-installer.org/en/latest/usage.html#pip-install
http://www.pip-installer.org/en/latest/logic.html#git
http://stackoverflow.com/questions/6947988/when-to-use-pip-requirements-file-versus-install-requires-in-setup-py
https://groups.google.com/d/msg/python-virtualenv/1eI6Z9_XRHE/cj6CCHvmS10J
http://stackoverflow.com/questions/2087148/can-i-use-pip-instead-of-easy-install-for-python-setup-py-install-dependen

#### requirements.txt

`from pip.req import parse_requirements`

http://stackoverflow.com/questions/14399534/how-can-i-reference-requirements-txt-for-the-install-requires-kwarg-in-setuptool?answertab=votes#answer-16624700

> Require pip>=1.2, as lower versions have a bug
https://github.com/erikrose/peep/commit/65367f66b777f17b1223569e1cd2f6250a820e99

#### 尽管提供了dependency_lins依然默认安装PyPi版本的坑
http://stackoverflow.com/questions/17366784/setuptools-unable-to-use-link-from-dependency-links/17442663#17442663
http://www.pip-installer.org/en/latest/logic.html#requirements-file-format

[Writing a Package in Python](http://www.packtpub.com/article/writing-a-package-in-python)
