---
title: 关闭/打开 Mac 开机声音
author: Q
type: post
date: 2015-10-17T14:06:48+00:00
url: /blog/760
views:
  - 1065
categories:
  - Mac
tags:
  - Mac

---
关闭声音：
```bash
sudo nvram StartupMute=%01
```

开启声音：
```bash
sudo nvram StartupMute=%00
```