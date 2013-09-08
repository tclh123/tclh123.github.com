---
layout: post
title: "prevent 'Adobe Reader Updater Helper' automatic run with system on OS X"
date: 2013-07-06 03:19
comments: true
categories: 
---

今天开机的时候发现Adobe Reader检查更新的进程自启动而且高CPU占用，不一会儿就弹出个更新提示窗口。

不爽之。

遂在 ~/Library/LaunchAgents 目录下发现 `com.adobe.ARM.202f4087f2bbde52e3ac2df389f53a4f123223c9cc56a8fd83a6f7ae.plist` 文件一枚，改后缀。。

文件内容是下面这样的。。
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.adobe.ARM.202f4087f2bbde52e3ac2df389f53a4f123223c9cc56a8fd83a6f7ae</string>
    <key>ProgramArguments</key>
    <array>
        <string>/Applications/Adobe Reader.app/Contents/MacOS/Updater/Adobe Reader Updater Helper.app/Contents/MacOS/Adobe Reader Updater Helper</string>
        <string>semi-auto</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>StartInterval</key>
    <integer>12600</integer>
</dict>
</plist>
```

在Adobe Reader程序[首选项里改](http://helpx.adobe.com/acrobat/kb/disable-automatic-updates-acrobat-reader.html)，也许也可以不弹出更新提示，但是不知道是否依然会有自启动的进程。

反正两边都弄了应该没事了~....

##Update

总结几个OS X潜在的自启动的地方。

- /Library/LaunchDaemons/
- /Library/LaunchAgents/
- ~/Library/LaunchAgents/
- /System/Library/StartupItems
- /Library/StartupItems
- GUI 的 Login Items（系统偏好，用户群组，登陆项），*找不到对应的文件？*

另外这两个是系统级的，

- /System/Library/LaunchDaemons/
- /System/Library/LaunchAgents/

Ps. 加载顺序应该是 Daemons->Agents->StartupItems（在/System/Library/LaunchDaemons/里可以找到com.apple.SystemStarter.plist，由com.apple.SystemStarter进程负责加载StartupItems）。

