---
title: macOS 终端使用代理 Proxy
author: Q
type: post
date: 2017-12-02T14:18:40+00:00
url: /blog/777
views:
  - 1632
categories:
  - Miscellaneous
tags:
  - GFW
  - linux
  - proxy

---
打开终端，运行：

```bash
vim ~/.bash_profile //使用bash
vim ~/.zprofile     //使用zsh
```

复制到 .bash_profile 或 .zprofile ：

```bash
export https_proxy=http://127.0.0.1:6152 //替换为你自己的代理 
export http_proxy=http://127.0.0.1:6152  //替换为你自己的代理 
```

保存配置，运行：

```bash
source ~/.bash_profile //使用bash
source ~/.zprofile     //使用zsh
```

该方法配置好后，在 Jetbrain 等 IDE 的终端下同样有用。