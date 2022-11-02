---
title: 'Windows 批处理文件 .bat  一键修改 DNS'
author: Q
type: post
date: 2019-12-28T13:00:19+00:00
url: /blog/908
wp_player_music_type:
  - netease
mp3_xiami_type:
  - song
wp_player_lyric_open:
  - close
toc_depth:
  - 1
i3geek_xzh_submit:
  - -1
views:
  - 4701
ampforwp-amp-on-off:
  - default
categories:
  - Miscellaneous
tags:
  - bat
  - DNS
  - Windows
  - 批处理

---
创建文件 dns.bat

```bash
@echo off
chcp 65001
netsh interface ip set dnsservers "以太网" static 114.114.114.114 primary
netsh interface ip add dnsservers "以太网" 8.8.8.8 index=2 
ipconfig /flushdns
```

右键-以管理员身份运行即可，以太网改为你的网络名称