---
title: 解决 Wordpress 域名隐藏 index.php 后子目录无法访问
author: Q
type: post
date: 2014-10-06T23:26:27+00:00
url: /blog/602
views:
  - 1287
categories:
  - Wordpress

---
以 Apache 为例，只需在 .htaccess 文件中添加一个规则，比如我有一个images目录，需要添加以下规则

```apache
RewriteRule /images/(.*) /images/$1 [L]
```