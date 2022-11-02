---
title: SSH 免 IP 用户名 连接
author: Q
type: post
date: 2018-02-26T13:32:08+00:00
url: /blog/925
wp_player_music_type:
  - netease
mp3_xiami_type:
  - song
wp_player_lyric_open:
  - close
ampforwp-amp-on-off:
  - default
i3geek_xzh_submit:
  - -1
views:
  - 1389
categories:
  - Linux
tags:
  - linux
  - SSH
  - VPS

---
配置服务器别名，使用别名代替 IP。

打开或新建 ~/.ssh/config 文件，输入以下内容：

```bash
Host server-alias     # server-alias为SSH链接的服务器别名，随便改自己的
  HostName server-ip  # 服务器 IP
  Port 22             # 端口
  User username       # 服务器端用户名
  PreferredAuthentications publickey 
  IdentityFile ~/.ssh/id_rsa   # 私钥，默认为 ~/.ssh/id_rsa
```

以后就可以通过以下命令连接 SSH

```bash
ssh server-alias
```