title: 如何制作USB启动盘
layout: post
date: 2015-10-17 20:45:31
tags: [USB, Linux, Command Line]
categories: develop
thumbnailImage: http://beginnerlinuxtutorial.com/wp-content/uploads/2014/05/live-Linux-USB.jpg
---
不需要光盘，U盘就可以用来安装操作系统。

<!-- more -->

`本文在Mac上操作，以ubuntu server为例`

# 到[ubuntu](http://www.ubuntu.com/download/server)管网下载相应的iso

# 转换iso为dmg格式
```shell
hdiutil convert -format UDRW -o /path/to/target /path/to/ubuntu.iso
```
# 插入U盘前后作下对比
```shell
diskutil list
```

# unmount USB
```shell
diskutil unmountDisk /dev/disk2
```

# 使用dd将镜像刷入USB
```shell
sudo dd if=/path/to/target.dmg of=/dev/rdiskN bs=1m
```

# 推出USB
```shell
diskutil eject /dev/diskN
```
