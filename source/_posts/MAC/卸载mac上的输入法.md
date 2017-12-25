---
title: 卸载mac上的输入法
date: 2017-01-21T22:30:05.000Z
tags: mac
---

mac电脑上,有的多余的输入法,发现竟然删不掉.每次切换输入法的时候总是要多按几次切换.表示极其的不爽.

首先就是系统默认的输入法.

## 系统输入法
* 安装Xcode或下载“Property List Editor”，因为需要打开(.plist)格式文件 

* 打开“终端”

* 在“终端”里输入命令
```
sudo open ~/Library/Preferences/com.apple.HIToolbox.plist
```
回车，输入用户账户的密码

![](http://www.cr173.com/up/2017-1/201701161151525689893.png)

我们选中“Root”—“AppleEnabledInputSources”， 一个一个点开,查找你想要删除的输入法，然后删除。

![](http://www.cr173.com/up/2017-1/201701161152373133375.png)

最后重启Mac


## QQ输入法等第三方输入法

* 首先打开活动监视器，把QQ输入法进程关闭。 

* Finder界面按下 shift+command+G, 输入：/library/input methods（系统的资料库）, 进入文件夹，找到qq输入法，删掉。 

* Finder界面按下 shift+command+G, 输入：~/library/input methods （个人文件夹的资料库）， 进入文件夹，找到qq输入法，删掉。