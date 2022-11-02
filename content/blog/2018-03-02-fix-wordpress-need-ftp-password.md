---
title: WordPress 需要访问您网页服务器的权限，需输入 FTP 的解决办法
author: Q
type: post
date: 2018-03-02T09:01:24+00:00
url: /blog/927
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
  - 1423
categories:
  - Wordpress
tags:
  - Apache
  - linux
  - WordPress

---
导致这个问题的根本原因还是文件夹权限的问题，而且不是访问、读取、写入这类的 777 权限，而是所属用户的用户权限，既然如此我们修改用户权限就可以解决了。

LAMP 环境下解决方法：

```bash
chown -R apache /data/www/xxx.com
```