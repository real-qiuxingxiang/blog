---
title: Python 批量按文件名关键字新建文件夹并归档文件
author: Q
type: post
date: 2022-03-27T03:39:32+00:00
url: /blog/1149
views:
  - 103
categories:
  - Programming
tags:
  - Python

---
按需求修改规则使用，现在代码的规则对应的文件名为：xxx-xxx-xxx-xxx-xxx-xxx.jpg。

```python
import os
import shutil

current_path = os.getcwd()
print('当前目录：'+current_path)

filename_list = os.listdir(current_path)
print('当前目录下文件：',filename_list)

print('正在分类整理进文件夹ing...')
for filename in filename_list:
    try:
        name1, name2, name3, name4, name5, name6 = filename.split('-') //规则
        dirName = name1 + "-" + name2 + "-" + name3 + "-" + name4 + "-" + name5 //规则
        try:
            os.mkdir(dirName)
            print('创建文件夹：' + dirName)
        except:
            pass
        try:
            shutil.move(current_path+'/'+filename, current_path+'/'+dirName)
            print(filename+'转移成功！')
        except Exception as e:
            print('移动失败:' + e)
    except:
        pass

print('整理完毕！')
```