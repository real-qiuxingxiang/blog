---
title: Python 3.7 + BeautifulSoup 4 + Scrapy ：简单爬虫实例
author: Q
type: post
date: 2018-07-26T13:15:47+00:00
url: /blog/962
ampforwp-amp-on-off:
  - default
views:
  - 3446
categories:
  - Programming
tags:
  - BeautifulSoup
  - Python
  - Scrapy
  - Spider
  - 爬虫

---
放假无聊，无聊写个爬虫，把本博客的文章列表页面（https://xingxiang.me/blog）扒下来

<!--more-->

## **1. Python 3.7 + BeautifulSoup 4**

输出 .csv 文件，如图：

![myblog_list](/images/myblog_list.png)

代码如下：

```python
import requests
import csv
import random
import time
import socket
import http.client
from bs4 import BeautifulSoup

def get_html(url, data = None):
    header = {
        'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8',
        'Accept-Encoding': 'gzip, deflate',
        'Accept-Language': 'zh-CN,zh;q=0.9,en;q=0.8,zh-TW;q=0.7',
        'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36'
    }
    timeout = random.choice(range(80, 100))
    while True:
        try:
            response = requests.get(url, headers = header, timeout = timeout)
            response.encoding = 'utf-8'
            break
        except socket.timeout as e:
            print(e)
            time.sleep(random.choice(range(20, 60)))
        except socket.error as e:
            print(e)
            time.sleep(random.choice(range(0, 60)))
        except http.client.BadStatusLine as e:
            print(e)
            time.sleep(random.choice(range(30, 60)))
        except http.client.IncompleteRead as e:
            print(e)
            time.sleep(random.choice(range(20, 60)))
    return response.text
    
def get_data(html_text):
    result = []
    bs = BeautifulSoup(html_text, "html.parser")
    content = bs.find_all('div', {'class': 'brick'})
    for blog in content:
        temp = []
        a_tag = blog.find('a')
        a_tag.span.extract()
        temp.append(a_tag['href'])
        temp.append(a_tag.text)
        result.append(temp)
    
    return result
    
def data_output(data, filename):
    with open(filename, 'a', errors='ignore', newline='') as f:
        f_csv = csv.writer(f)
        f_csv.writerows(data)
        
if __name__ == '__main__':
    url = 'https://xingxiang.me/blog'
    html = get_html(url)
    result = get_data(html)
    data_output(result, 'blog.csv')
```

## 2.Python 3.7 + Scrapy

输出 .json 文件，如图：

![myblog_json](/images/myblog_json.png)

代码如下

```python
#myblog_spider.py
import scrapy
from myblog_spider.items import MyblogSpiderItem

class myBlogSpider(scrapy.Spider):
	name = 'myBlogSpider'
	allow_domains = ['xingxiang.me']
	start_urls = ["https://xingxiang.me/blog"]

	def parse(self, response):
		for blog in response.xpath('//div[@class="brick"]/a'):
			item = MyblogSpiderItem()
			item['url'] = blog.xpath('@href').extract_first()
			item['title'] = blog.xpath('text()').extract_first()
			yield item
```

```python
#items.py
import scrapy

class MyblogSpiderItem(scrapy.Item):
	# define the fields for your item here like:
	# name = scrapy.Field()
	title = scrapy.Field()
	url = scrapy.Field()
	pass
```

```python
#pipelines.py
import codecs
import json

class MyblogSpiderPipeline(object):
	def __init__(self):        
		self.file = codecs.open('logs.json', 'w', encoding='utf-8')
	def process_item(self, item, spider):
		line = json.dumps(dict(item), ensure_ascii=False) + "\n"
		self.file.write(line)
		return item
	def spider_closed(self, spider):
		self.file.close()
```