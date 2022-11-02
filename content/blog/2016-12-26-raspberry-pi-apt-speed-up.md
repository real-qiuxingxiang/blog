---
title: 树莓派apt加速 替换apt源为国内镜像
author: Q
type: post
date: 2016-12-26T06:32:27+00:00
url: /blog/838
views:
  - 1838
categories:
  - Linux
tags:
  - RaspberryPi
  - 树莓派

---

因为众所周知的原因，Linux默认的apt源在国内神慢……换吧

1.改sources.list
```bash
sudo vim /etc/apt/sources.list
```

内容全部改为
```bash
deb http://mirrors.ustc.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi
#deb-src http://mirrors.ustc.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi
```

2.改raspi.list
```bash
sudo vim /etc/apt/sources.list.d/raspi.list
```

内容全部改为
```bash
deb http://mirrors.ustc.edu.cn/archive.raspberrypi.org/debian/ buster main ui
deb-src http://mirrors.ustc.edu.cn/archive.raspberrypi.org/debian/ buster main ui
```

## 爽快！