---
title: Windows 批量将子目录文件移动到根目录 bat
author: Q
type: post
date: 2022-03-27T03:31:00+00:00
url: /blog/1148
views:
  - 115
categories:
  - Windows
tags:
  - Windows

---
放到包含一堆子文件夹的文件根目录运行。

```powershell
@echo off
for /f "delims=" %%a in ('dir /a-d /b /s ') do (move "%%~a" ./)
```