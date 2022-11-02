---
title: Dell XPS 15 9550 黑苹果 macOS Catalina 双系统 不用 U 盘
author: Q
type: post
date: 2020-02-27T06:53:21+00:00
url: /blog/1021
ampforwp-amp-on-off:
  - default
views:
  - 3154
categories:
  - Mac
tags:
  - Hackintosh
  - macOS
  - XPS
  - 黑苹果

---
因为疫情原因，在家闲的慌，想折腾一下 Hackintosh，但是手头上没有 U 盘，就想看看能不能不用 U 盘安装黑苹果。

其实完全是可以的，参见：[macOS Catalina 10.15.6(17G73)恢复版系统镜像包][1]

这个方法类似以前的 ghost 镜像，恢复硬盘，安装完后建议新建一个用户，把原来的用户删除。

最重要的还是 EFI 分区的配置，上面的镜像是通用的，Clover 则是根据每一部机器定制的。

## XPS 9550 的 Clover：

<https://github.com/xxxzc/xps15-9550-macos> （我根据这个修改）

<https://github.com/krim404/DellXPS15-9550-OSX>

 [1]: http://k61.org/b960947f.html