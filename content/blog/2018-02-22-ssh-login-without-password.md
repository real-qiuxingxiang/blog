---
title: SSH 免密码登录 ssh-copy-id 命令
author: Q
type: post
date: 2018-02-22T13:19:33+00:00
url: /blog/923
views:
  - 991
categories:
  - Linux
tags:
  - CentOS
  - linux
  - SSH

---
如果你管理一台 Linux Server，那么你就会知道每次 SSH 登录时或者使用 scp 复制文件时都要输入密码是一个多么繁琐的过程，免密码登陆其实很简单。

SSH无密码登录的设置步骤：

## 1.本地 Linux 生成 SSH 密钥和 SSH 公钥

首先我们在自己的 Linux 系统上生成一对 SSH Key：SSH密钥和SSH公钥。密钥保存在自己的Linux系统上。

然后公钥上传到 Linux Server，之后我们就能无密码SSH登录了。

打开终端，使用下面的 ssh-keygen 来生成 RSA 密钥和公钥．-t表示type，就是说要生成RSA加密的钥匙．

```bash
ssh-keygen -t rsa
```

RSA也是默认的加密类型．所以你也可以只输入 ssh-keygen。默认的RSA长度是2048位，也可以指定 4096 位长度．

```bash
ssh-keygen -b 4096 -t rsa
```

生成 SSH Key 的过程中会要求你指定一个文件来保存密钥，按Enter键使用默认即可。然后需要输入一个密码来加密你的SSH Key。  
SSH 密钥会保存在 home 目录下的.ssh/id_rsa 文件中。  
SSH公钥保存在.ssh/id_rsa.pub文件中．

```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/home/matrix/.ssh/id_rsa): 　按Enter键
Enter passphrase (empty for no passphrase): 　　输入一个密码
Enter same passphrase again: 　　再次输入密码
Your identification has been saved in /home/matrix/.ssh/id_rsa.
Your public key has been saved in /home/matrix/.ssh/id_rsa.pub.
The key fingerprint is:
e1:dc:ab:ae:b6:19:b0:19:74:d5:fe:57:3f:32:b4:d0 matrix@vivid
The key's randomart image is:
+---[RSA 4096]----+
| .. |
| . . |
| . . .. . |
| . . o o.. E .|
| o S ..o ...|
| = ..+...|
| o . . .o .|
| .o . |
| .++o |
+-----------------+
```

## ２将 SSH 公钥上传到Linux服务器

可以使用ssh-copy-id命令来完成。

```bash
ssh-copy-id username@remote-server
```

SSH公钥会自动上传。

SSH公钥保存在远程Linux服务器的 .ssh/authorized_keys

大功告成