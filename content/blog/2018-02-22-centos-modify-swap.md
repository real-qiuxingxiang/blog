---
title: 'CentOS: 增加/调整 Swap 大小'
author: Q
type: post
date: 2018-02-22T12:23:43+00:00
url: /blog/922
views:
  - 1644
categories:
  - Linux
tags:
  - CentOS
  - linux

---
第一步：关闭 Swap

```bash
sudo swapoff -a
```
  
第二步：把当前的 Swap 文件增大

```bash
sudo dd if=/dev/zero of=/swapfile bs=1M count=1024
```

bs 指的是 Block Size，就是每一块的大小。这里是 1M，意思就是 count 以 1M 为单位的。  
count 就是新的 swapfile 要多少个 block。这里是1024，就是说，新的 Swap 大小为 1Gb。


第三步：把增大后的文件变为 Swap 文件。

```bash
sudo mkswap /swapfile
```

第四步：重新打开 Swap

```bash
sudo swapon /swapfile
```

第五步：让 Swap 在启动的时候，自动生效。打开 /etc/fstab 文件

```bash
sudo vim /etc/fstab
```

第六步：再vim里，加上以下命令。然后保存。

```bash
/swapfile swap swap defaults 0 0
```