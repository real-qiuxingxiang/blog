---
title: Ubuntu 上制作 .deb 详细图文教程
author: Q
type: post
date: 2013-05-31T06:27:17+00:00
url: /blog/463
views:
  - 4422
categories:
  - iOS
  - Jailbreak
tags:
  - deb
  - dpkg
  - iOS
  - Ubuntu

---
如何汉化插件？ 请看我的第一篇教程： <https://xingxiang.me/blog/466/> 

## 首先认识一下什么是.deb

deb 是 Unix 系统(其实主要是 Linux )下的安装包，基于 tar 包，因此本身会记录文件的权限(读/写/可执行)以及所有者/用户组。

由于 Unix 类系统对权限、所有者、组的严格要求，而 deb 格式安装包又经常会涉及到系统比较底层的操作，所以权限等的设置尤其重要。

## deb 包本身有三部分组成：

1.数据包，包含实际安装的程序数据，文件名为 data.tar.XXX；

2.安装信息及控制脚本包，包含 deb 的安装说明，标识，脚本等，文件名为 control.tar.gz；

3.最后一个是 deb 文件的一些二进制数据，包括文件头等信息，一般看不到，在某些软件中打开可以看到。

deb 本身可以使用不同的压缩方式。tar 格式并不是一种压缩格式，而是直接把分散的文件和目录集合在一起，并记录其权限等数据信息。之前提到过的 data.tar.XXX，这里 XXX 就是经过压缩后的后缀名。deb 默认使用的压缩格式为 gzip 格式，所以最常见的就是 data.tar.gz。常有的压缩格式还有 bzip2 和 lzma，其中 lzma 压缩率最高，但压缩需要的 CPU 资源和时间都比较长。

data.tar.gz包含的是实际安装的程序数据，而在安装过程中，该包里的数据会被直接解压到根目录(即 / )，因此在打包之前需要根据文件所在位置设置好相应的文件/目录树。

而 control.tar.gz 则包含了一个 deb 安装的时候所需要的控制信息。一般有 5 个文件：

control，用了记录软件标识，版本号，平台，依赖信息等数据；

preinst，在解包 data.tar.gz 前运行的脚本；

postinst，在解包数据后运行的脚本；

prerm，卸载时，在删除文件之前运行的脚本；

postrm，在删除文件之后运行的脚本；

在 Cydia 系统中，Cydia 的作者 Saurik 另外添加了一个脚本，extrainst_，作用与 postinst 类似。

## 准备工作：

Ubuntu 13.10 下载地址：<http://www.ubuntu.org.cn/download/desktop>

![][1]

建议直接在电脑上安装，不要用虚拟机

认识dpkg-deb命令（查看大图）

![][2]

control模板：

```
Package: app.weiphone.qxxqxx
Name:&nbsp;&nbsp;deb的名字，可以是中文
Version: 1.0
Architecture: iphoneos-arm&nbsp;&nbsp;
Depends:
Description:&nbsp;&nbsp;描述
Maintainer: 维护人
Author: qxxqxx &lt;&gt;
 ==================================================================================================== 
```

## Part One 解包

1. Alt+crtl+t 打开终端

![][3]

2. 首先要有一个deb 这里的是weiphone源图标 方便演示放到桌面

![][4]

3. 在终端 用ls 和 cd 命令定位到桌面和查看桌面的文件

![][5]

4. 解包.deb

dpkg-deb -e

dpkg-deb -x

输入第一条命令

![][6]

回车后，在1 文件夹里，就是deb的主文件了

![][7]

输入第二条命令

![][8]

回车后，在1 文件夹里，就是deb的DEBIAN文件夹

![][9]

至此。一个deb就被完全解包了。

## Part Two 打包制作deb

首先了解一下deb的原理

deb包里有和在ios里路径一样的文件夹（大家自己随便解包一个来看看）。安装时就是把deb里面的文件覆盖或复制到deb包里面文件夹的路径，ios里已经有的就覆盖，无则复制（但是如果是其它不同的DEB包安装的就会提示冲突）(不同的deb包指的是包名不同)。所以下面的教程将举几个例子给大家看，包简单明了！！！！！

打包deb需要一个命令： dpkg-deb -b

还需要用到一个必须的control文件

### 例子1： 简单制作一个deb，把一个文件通过deb放到指定路径

1.首先，新建一个文件夹

![][10]

2. 要把某文件复制到 /var/mobile ，so新建一个对应路径的文件夹

![][11]

3. 把要复制的设备的文件放到文件夹里

![][12]

4. 回到根目录，新建一个DEBIAN文件夹，注意大小写

![][13]

5.在DEBIAN里新建一个文本文档，名为control

![][14]

编辑control，下面的编码选 pkg-config （control文件最后一行必须至少有一个换行的空行）

control文件必须是UTF-8，Unix编码，Unix/Linux换行符（LF），不符合规范的control会导致Cydia无法打开。

![][15]

## 6. 回到桌面，打开终端，开始打包

DEBIAN文件夹的权限应为：755

chmod 755 ./例子1/DEBIAN

输入命令

![][16]

完成后

![][17]

大家可以安装到机子里看看

### 例子2 制作插件汉化补丁

已开新贴：<https://xingxiang.me/blog/465/>

 [1]: /images/ubuntu-deb/1.png
 [2]: /images/ubuntu-deb/2.png
 [3]: /images/ubuntu-deb/3.png
 [4]: /images/ubuntu-deb/4.png
 [5]: /images/ubuntu-deb/5.png
 [6]: /images/ubuntu-deb/6.png
 [7]: /images/ubuntu-deb/7.png
 [8]: /images/ubuntu-deb/8.png
 [9]: /images/ubuntu-deb/9.png
 [10]: /images/ubuntu-deb/10.png
 [11]: /images/ubuntu-deb/11.png
 [12]: /images/ubuntu-deb/12.png
 [13]: /images/ubuntu-deb/13.png
 [14]: /images/ubuntu-deb/14.png
 [15]: /images/ubuntu-deb/15.png
 [16]: /images/ubuntu-deb/16.png
 [17]: /images/ubuntu-deb/17.png