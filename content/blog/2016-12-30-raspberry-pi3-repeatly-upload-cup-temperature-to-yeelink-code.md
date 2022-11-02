---
title: 树莓派3 定时上传CUP温度到 yeelink 代码
author: Q
type: post
date: 2016-12-30T13:24:03+00:00
url: /blog/842
views:
  - 1454
categories:
  - Programming
tags:
  - RaspberryPi
  - 树莓派

---
CPUtemperature.py 代码

```python
#!/usr/bin/env python  

import requests  
import json  
import time  

file = open("/sys/class/thermal/thermal_zone0/temp")  
CPUtemperature = float(file.read()) / 1000  
file.close

print "CPU Temperature :", CPUtemperature

topost_CPUtemperature_payload={'value':CPUtemperature}

url_CPUtemperature='你的传感器URL' 
header={'U-ApiKey':'你的Apikey', 'content-type': 'application/json'}

post_CPUtemperature = requests.post(url_CPUtemperature,headers=header,data=json.dumps(topost_CPUtemperature_payload))
```

yeelink.sh 代码

```bash
sudo python /home/pi/yeelink.py
```

运行
```bash
sudo chmod +x /home/pi/yeelink.sh
```

设置定时5分钟运行一次
```bash
sudo crontab -e
```

加入
```bash
*/5 * * * * /home/pi/yeelink.sh
```