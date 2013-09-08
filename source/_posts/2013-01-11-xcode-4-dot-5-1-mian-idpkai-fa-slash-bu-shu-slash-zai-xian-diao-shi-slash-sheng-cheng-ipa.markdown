---
layout: post
title: "xcode 4.5.1 免iDP开发/部署/在线调试/生成ipa"
date: 2013-01-11 14:45
comments: true
categories: ipad ios xcode iDP hack
---

本文是结合自己测试的情况，对 [这篇教程](http://kqwd.blog.163.com/blog/static/4122344820117191351263/) 的整理，针对 xcode 4.5.1。

### 1. 修改 SDKSettings.plist

``` bash
cd /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS6.0.sdk

sudo cp SDKSettings.plist SDKSettings.plist.orig

sudo cp SDKSettings.plist /tmp/SDK.plist

sudo chmod 777 /tmp/SDK.plist

sudo /Applications/Xcode.app/Contents/MacOS/Xcode /tmp/SDK.plist
```
    
展开DefaultProperties分支，将下面的 CODE_SIGNING_REQUIRED、ENTITLEMENTS_REQUIRED 两个属性改为NO

``` bash
sudo cp /tmp/SDK.plist SDKSettings.plist
```

### 2. 修改 Info.plist

``` bash
cd /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform

sudo cp Info.plist Info.plist.orig

sudo cp Info.plist /tmp/Info.plist

sudo chmod 777 /tmp/Info.plist

sudo /Applications/Xcode.app/Contents/MacOS/Xcode /tmp/Info.plist
```

将 DefaultProperties、RuntimeRequirements、OverrideProperties分支下 的 XCiPhoneOSCodeSignContext 修改成 XCCodeSignContext。

``` bash
sudo cp /tmp/Info.plist Info.plist
```

### 3. 执行脚本

``` bash
#!/bin/bash
cd /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/PrivatePlugIns/iPhoneOS\ Build\ System\ Support.xcplugin/Contents/MacOS/
dd if=iPhoneOS\ Build\ System\ Support of=working bs=500 count=255
printf "xc3x26x00x00" >> working
/bin/mv -n iPhoneOS\ Build\ System\ Support iPhoneOS\ Build\ System\ Support.original
/bin/mv working iPhoneOS\ Build\ System\ Support
chmod a+x iPhoneOS\ Build\ System\ Support
```

正常的话应该输出(具体的数字可能有差别)

```bash
231+1 records in
231+1 records out
115904 bytes transferred in 0.001738 secs (66694555 bytes/sec)
```

### 4. 获取 gen_entitlements.py

需要连网执行

``` bash
mkdir /Applications/Xcode.app/Contents/Developer/iphoneentitlements
cd /Applications/Xcode.app/Contents/Developer/iphoneentitlements
curl -O http://www.alexwhittemore.com/iphone/gen_entitlements.txt
mv gen_entitlements.txt gen_entitlements.py
chmod 777 gen_entitlements.py
```

### 5. 禁用Xcode自动的签名操作

*这个似乎不做也行*

将工程配置中所有的Code Signing选项全部设为Don't Code Sign，如图。可能需要先点击“All”让这个选项显示出来

### 6. 添加自定义的生成后脚本

在Build Phases中添加一个Phase，右下角的Add Build Phase，然后单击Add Run Script，输入以下脚本

``` bash
export CODESIGN_ALLOCATE=/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin/codesign_allocate
if [ "${PLATFORM_NAME}" == "iphoneos" ] || [ "${PLATFORM_NAME}" == "ipados" ]; then
/Applications/Xcode.app/Contents/Developer/iphoneentitlements/gen_entitlements.py "my.company.${PROJECT_NAME}" "${BUILT_PRODUCTS_DIR}/${WRAPPER_NAME}/${PROJECT_NAME}.xcent";
codesign -f -s "iPhone Developer" --entitlements "${BUILT_PRODUCTS_DIR}/${WRAPPER_NAME}/${PROJECT_NAME}.xcent" "${BUILT_PRODUCTS_DIR}/${WRAPPER_NAME}/"
fi
```

> ###旁门左道生成IPA文件

> 如果我的程序调试好了，怎么才能发给别人用呢？正常情况下IPA文件是从Xcode的Organizer中输出的，但是我们没有证书，这样输出会产生错误。我们只能用个小trick来完成这个操作了。

> 先将代码生成为Release目标，然后打开工程的输出文件夹，通常情况下这个目录是
/Users/你的用户名/Library/Developer/Xcode/DerivedData/以工程名打头的文件夹/Build/Products/Release-iphoneos

> 很纠结吧~这个目录下有个.app的文件，就是生成的程序了。把这个.app拖到iTunes中，它会出现在应用程序那个列表中，然后再把它从iTunes的那个列表中拖出来（比如拖到桌面），发生了什么？哈哈，它就这样变成.ipa了！

PS.

我的 ipad 还是 ios5.1 的，好像运行有点错误。不知道是不是应该用5.1的SDK。

* [How can I add older version of iOS SDK in Xcode 4.5](http://stackoverflow.com/questions/12523888/how-can-i-add-older-version-of-ios-sdk-in-xcode-4-5)