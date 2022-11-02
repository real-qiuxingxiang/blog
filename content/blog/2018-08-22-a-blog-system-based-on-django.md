---
title: 基于Django 开发的博客系统
author: Q
type: post
date: 2018-08-22T07:50:40+00:00
url: /blog/975
ampforwp-amp-on-off:
  - default
views:
  - 2331
categories:
  - Programming
tags:
  - Django
  - Python

---
  * Python 3.6.6 和 Django 2.1.5
  * MySQL
  * [xadmin][1] 后台管理
  * [Simditor Markdown][2] 编辑器，图片 Drag and Drop 上传
  * 代码高亮
  * RSS订阅
  * 标签、阅读量
  * [haystack][3] 文章内容搜索
  * [Valine][4] 评论系统
  * 集成 django-compressor，静态文件压缩


### Usage

  * 新建虚拟环境

```bash
git clone git@github.com:chiuxingxiang/Django-Blog.git
virtualenv --python=&lt;py3path> venv
. venv/bin/activate
```

  * 安装依赖
	
```bash
pip install -r requirements.txt
```

  * 数据库迁移
```bash
python manage.py makemigrations
python manage.py migrate
```

  * 创建管理员
```bash
python manage.py shell
from django.contrib.auth.models import User
user=User.objects.create_superuser('用户名','邮箱','密码')
```

  * 创建搜索索引
```bash
python manage.py rebuild_index
```

  * 压缩静态文件
```bash
python manage.py collectstatic
python manage.py compress
```
### 首页

![index][5] 

### 详情页 + 评论

![detail][6] 

### Tag List

![tag_list][7] 

### xadmin后台

![admin][8] 

### Simditor Markdown 文章编辑器 图片上传

![pic_upload][9]

 [1]: https://github.com/sshwsfc/xadmin
 [2]: https://github.com/istommao/django-simditor
 [3]: https://github.com/django-haystack/django-haystack
 [4]: https://github.com/xCss/Valine
 [5]: /images/github_pic/index.png ""
 [6]: /images/github_pic/detail.png ""
 [7]: /images/github_pic/tag.png
 [8]: /images/github_pic/admin.png
 [9]: /images/github_pic/pic_upload.png ""