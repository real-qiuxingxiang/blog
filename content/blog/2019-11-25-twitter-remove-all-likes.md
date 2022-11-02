---
title: Twitter 取消所有喜欢
author: Q
type: post
date: 2019-11-25T09:35:15+00:00
url: /blog/991
ampforwp-amp-on-off:
  - default
views:
  - 4297
categories:
  - Linux
tags:
  - Twitter

---
用 Chrome 打开 Twitter 网页版 Like 页面，在 Console 运行以下脚本，等待便可：

```javascript
setInterval(() => {
  for (const d of document.querySelectorAll('div[data-testid="unlike"]')) {
    d.click()
  }
  window.scrollTo(0, document.body.scrollHeight)
}, 1000)
```