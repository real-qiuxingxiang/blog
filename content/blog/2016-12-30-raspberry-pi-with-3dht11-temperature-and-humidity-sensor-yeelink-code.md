---
title: 树莓派3 + DHT11 温湿度传感器 + 定时上传 yeelink 代码 + 数据过滤
author: Q
type: post
date: 2016-12-30T01:19:44+00:00
url: /blog/840
views:
  - 1951
categories:
  - Programming
tags:
  - RaspberryPi
  - 树莓派

---
DHT11.py 代码

```python
#!/usr/bin/python

import RPi.GPIO as GPIO
import time
import requests
import json

#Read data from DHT11
def DHT11():
  channel = 17
  data = []
  j = 0

  GPIO.setmode(GPIO.BCM)
  time.sleep(1)
  GPIO.setup(channel, GPIO.OUT)
  GPIO.output(channel, GPIO.LOW)
  time.sleep(0.02)
  GPIO.output(channel, GPIO.HIGH)
  GPIO.setup(channel, GPIO.IN)

  while GPIO.input(channel) == GPIO.LOW:
       continue

  while GPIO.input(channel) == GPIO.HIGH:
       continue

  while j &lt; 40:
       k = 0
       while GPIO.input(channel) == GPIO.LOW:
           continue

       while GPIO.input(channel) == GPIO.HIGH:
           k += 1
           if k > 100:
               break
       if k &lt; 8:
           data.append(0)
       else:
           data.append(1)

       j += 1

  #print "sensor is working."
  #print data

  humidity_bit = data[0:8]
  humidity_point_bit = data[8:16]
  temperature_bit = data[16:24]
  temperature_point_bit = data[24:32]
  check_bit = data[32:40]

  global humidity
  global temperature
  global check
  humidity_point = 0
  temperature_point = 0
  check = 0
  temperature = 0
  humidity = 0

  for i in range(8):
       humidity += humidity_bit[i] * 2 ** (7 - i)
       humidity_point += humidity_point_bit[i] * 2 ** (7 - i)
       temperature += temperature_bit[i] * 2 ** (7 - i)
       temperature_point += temperature_point_bit[i] * 2 ** (7 - i)
       check += check_bit[i] * 2 ** (7 - i)

  global tmp
  tmp = humidity + humidity_point + temperature + temperature_point
  GPIO.cleanup()

def yeelink():
  print "DHT11 Temperature & Humidity Sensor"
  print "temperature :", temperature, "*C, humidity :", humidity, "%"

  mytemp = '%f' %temperature
  myhumi = '%f' %humidity

  topost_tmp_payload={'value':mytemp}
  topost_humidity_payload={'value':myhumi}

  url_tmp='你的传感器URL' 
  url_humidity='你的传感器URL'
  header={'U-ApiKey':'你的Apikey', 'content-type': 'application/json'}

  post_tem = requests.post(url_tmp,headers=header,data=json.dumps(topost_tmp_payload))
  post_humidity = requests.post(url_humidity,headers=header,data=json.dumps(topost_humidity_payload))

DHT11()
#Ignore the bad data
while check != tmp:
    DHT11()
yeelink() 
```

DHT11.sh 代码
```bash
sudo python /home/pi/DHT11.py
```

运行
```bash
sudo chmod +x /home/pi/DHT11.sh
```

设置定时5分钟运行一次
```bash
sudo crontab -e
```

加入
```bash
*/5 * * * * /home/pi/DHT11.sh
```