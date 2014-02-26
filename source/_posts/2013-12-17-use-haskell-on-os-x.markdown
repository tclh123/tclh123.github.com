---
layout: post
title: "use haskell on OS X"
date: 2013-12-17 14:54
comments: true
categories: Haskell
---


现在不用一个个装 GHC、Cabal 什么的了，直接装 [Haskell Platform](http://www.haskell.org/platform/mac.html).

装完1.2G...略忧伤

下面抄一下介绍..

## Haskell Platform for Mac OS X

Welcome to Haskell Platform. The platform consists of the Glasgow Haskell Compiler (GHC) and an extensive set of standard libraries and utilities with full documentation.

### Documentation

- Libraries
    Documentation for the libraries that come with Haskell Platform & GHC.
- GHC
    The GHC User's Guide has all you need to know about using GHC: command line options, language extensions, GHCi, etc.
- GHC API
    Documentation for the GHC API.
- Cabal
    An infrastructure for building and distributing Haskell software.
- Haddock
    A tool for automatically generating documentation from annotated Haskell source code.

### What is Installed

On Mac OS X, the Haskell Platform is installed in two major pieces: GHC and Haskell Platform. They are installed respectively in:

    /Library/Frameworks/GHC.framework
    /Library/Haskell

Executables are symlinked in /usr/bin and should be available in any shell.

### Uninstallation

This and prior versions of GHC and Haskell Platform can be found and then easily removed with the uninstallation command line utility:

    /Library/Haskell/bin/uninstall-hs

Simply run it for more information.

### Configuring Cabal

The cabal command manages the building and installation of packages, both your own, and those it can fetch from the Hackage repository.
The first time you run cabal, a Mac specific configuration is written into the ~/.cabal directory.

- If this is the first time you have ever run cabal, it will be made your active configuration.
- If you have run cabal in the past, the new settings are in the file config.platform. You might want to review and incorporate some of the settings into your existing config file, or just replace your config file with it entirely.

The configuration sets up cabal to install packages with the same layout as those installed with the Platform. Packages installed per user (--user, the default) are placed in a parallel tree in ~/Library/Haskell.

N.B. Built executables will be symlink'd into ~/Library/Haskell/bin, you probably want to add that to your $PATH by adding this line to your ~/.bash_profile:

    export PATH="$HOME/Library/Haskell/bin:$PATH"
