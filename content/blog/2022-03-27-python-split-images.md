---
title: Python 批量分割裁剪图片
author: Q
type: post
date: 2022-03-27T03:20:01+00:00
url: /blog/1147
views:
  - 95
categories:
  - Programming
tags:
  - Python

---
放到图片目录下运行，以下代码为从中间将图片一分为二，请根据自己需要修改。

```python
from PIL import Image
import os

path = os.getcwd()
print('当前目录：'+path)
path_list = os.listdir(path)
print(path_list)

j=1

for i in path_list:
    a = open(os.path.join(path,i),'rb')
    img = Image.open(a)
    w = img.width
    h = img.height
    print('正在处理图片',i,'宽',w,'长',h)

    box1 = (0,0,w*0.5,h) 
    img1 = img.crop(box1)
    box2 = (w*0.5,0,w,h)
    img2 = img.crop(box2)

    img1.save(str(j)+'.jpg', dpi=img1.info["dpi"])
    j = j + 1
    img2.save(str(j)+'.jpg', dpi=img2.info["dpi"])
    j = j + 1
```