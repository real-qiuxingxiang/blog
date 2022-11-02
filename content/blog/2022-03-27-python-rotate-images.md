---
title: Python 批量旋转图片
author: Q
type: post
date: 2022-03-27T03:17:43+00:00
url: /blog/1145
views:
  - 80
categories:
  - Programming
tags:
  - Python

---
放到图片目录下运行。

```python
from PIL import Image
import os

path = os.getcwd()
print('当前目录：'+path)
path_list = os.listdir(path)
print(path_list)

for i in path_list:
    a = open(os.path.join(path,i),'rb')
    img = Image.open(a)
    w = img.width
    h = img.height
    print('正在处理图片',i,'宽',w,'长',h)
    if h > w:
        img.rotate(180, expand=True).save('0'+i, dpi=img.info["dpi"])
        print('旋转成功')
    
print("'{}'目录下所有图片已经保存到本文件目录下。".format(path))
```