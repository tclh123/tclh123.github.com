---
layout: post
title: "setup raspberry pi on OS X"
date: 2013-10-04 21:53
comments: true
categories: pi
---

折腾了下树莓派，买了 PL2303串口TTL下载线，跟一个8G C10的TF带SD卡套。

只能串口访问，没买usb无线，没有多余网线。。不能SSH、开VNC。。不幸福

等能联网了再来折腾吧 →_→

---

## setup the SD card

- 用DiskUtil把sd卡erase成ExFat格式
- 执行 `df -h` 来获得sd卡的设备路径
- 将系统img写入sd卡

``` sh
tclh123@tclh123MBP ~ $ sudo dd bs=1m if="/path/to/2013-09-25-wheezy-raspbian.img" of=/dev/rdisk2
Password:
2825+0 records in
2825+0 records out
2962227200 bytes transferred in 168.735466 secs (17555451 bytes/sec)
```

And you can use `killall -INFO dd` to check the status of `dd` in  progress ([link](http://www.commandlinefu.com/commands/view/5440/check-the-status-of-dd-in-progress-os-x))

## 串口通信

- 下载PL2303串口驱动

http://www.prolific.com.tw/US/ShowProduct.aspx?p_id=229&pcid=41
安装完需要重启。。

- 下个minicom

`brew install minicom`

ps. 我不知道为什么直接用screen连 `screen /dev/tty.usbserial 9600` 会乱码加卡死。。
