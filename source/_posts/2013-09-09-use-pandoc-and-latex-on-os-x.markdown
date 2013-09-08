---
layout: post
title: "use Pandoc and LaTeX on OS X"
date: 2013-09-09 02:11
comments: true
categories: LaTeX
---

## Installing

- [Pandoc](http://code.google.com/p/pandoc/downloads/)
- MacTeX's [BasicTeX.pkg](http://www.tug.org/mactex/morepackages.html)

> For PDF output, you’ll also need LaTeX. We recommend installing BasicTeX (64M), and using the tlmgr tool to install additional packages as needed.

Just download and run the pkg files.

Then add `/usr/texbin` to your $PATH(`export PATH=${PATH}:/usr/texbin;`).

Now, you get them installed.

``` bash
pandoc --version

pdflatex -v
```

### Install tlmgr

[tlmgr - TeX Live package manager](http://www.tug.org/texlive/tlmgr.html)

``` bash
curl http://ftp.ctex.org/mirrors/CTAN/systems/texlive/tlnet/update-tlmgr-latest.sh -O
chmod a+x update-tlmgr-latest.sh
./update-tlmgr-latest.sh
```

``` bash My Output
Verifying archive integrity... All good.
Uncompressing TeX Live Manager Updater...........................................................................................................................................................................................
./runme.sh: updating in /usr/local/texlive/2013basic...
./runme.sh: tlmgr version says this is TeX Live 2013
./runme.sh: proceeding with tlmgr update.
D:tlmgr:main: ::tldownload_server defined
D:Using shipped /usr/local/texlive/2013basic/tlpkg/installer/wget/wget.x86_64-darwin for wget (tested).
D:Using shipped /usr/local/texlive/2013basic/tlpkg/installer/xz/xzdec.x86_64-darwin for xzdec (tested).
D:Using shipped /usr/local/texlive/2013basic/tlpkg/installer/xz/xz.x86_64-darwin for xz (not tested).
./runme.sh: done.
```

and you can check the version by `tlmgr --version`

``` bash setting default package repository
sudo tlmgr option location http://mirror.ctan.org/systems/texlive/tlnet/
```

## Simple Usage

``` bash
pandoc test1.md -s -o test1.pdf
```


**TO be continued**

##Reference
- https://github.com/mwhite/resume
- http://tug.ctan.org/
- http://www.ctan.org/tex-archive/fonts/tex-gyre/
- http://www.ctan.org/tex-archive/macros/latex/contrib/titlesec
- http://tex.stackexchange.com/questions/10706/pdftex-error-font-expansion-auto-expansion-is-only-possible-with-scalable
- http://www.tug.org/mactex/morepackages.html
- http://www.tug.org/texlive/
- http://cmwelsh.com/beautiful-resumes-with-markdown-and-latex
- http://sysadvent.blogspot.jp/2011/12/day-14-write-your-resume-in-markdown.html
