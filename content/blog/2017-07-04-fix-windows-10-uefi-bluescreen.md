---
title: Windows 10 UEFI 引导错误 蓝屏
author: Q
type: post
date: 2017-07-04T14:58:49+00:00
url: /blog/877
views:
  - 4033
categories:
  - Windows
tags:
  - Windows

---
修复如图错误

![uefi_bluescreen](/images/uefi_bluescreen.jpg)

## UEFI引导基本原理

### 1.ESP引导分区

ESP磁盘分区是GPT格式硬盘放EFI引导文件的磁盘，在MBR格式硬盘中也可以由任一fat  
格式磁盘分区代替

### 2.EFI文件结构

```bash
efi\boot\bootx64.efi
efi\microsoft\boot\bcd
```

### 3.EFI启动过程

UEFI Bios启动时，自动查找硬盘下ESP分区的bootx64.efi，然后由bootx64.efi引导  
EFI下的BCD文件，由BCD引导指定系统文件（一般为C:\windows\system32\winload.efi）

## 使用 bcdboot 命令修复

1.启动64bit WindowsPE，Bios/UEFI启动进入下都可以  
2.启动64位8PE，并用ESP分区挂载器或Diskgenuis挂载ESP分区  
3.打开cmd，输入以下命令并运行

```bash
bcdboot c:\windows /s o: /f uefi /l zh-cn
```

其中：

```bash
c:\windows  硬盘系统目录，根据实际情况修改
/s o:     指定esp分区所在磁盘，根据实际情况修改
/f uefi   指定启动方式为uefi
/l zh-cn  指定uefi启动界面语言为简体中文
注：64位7PE不带/s参数，故7PE不支持bios启动下修复
```