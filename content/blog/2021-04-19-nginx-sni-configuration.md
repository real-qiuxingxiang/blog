---
title: nginx SNI 配置
author: Q
type: post
date: 2021-04-19T09:36:01+00:00
url: /blog/1095
views:
  - 283
categories:
  - Linux
tags:
  - nginx

---
Server Name Indication (SNI) ，也被称为<a rel="noreferrer noopener" target="_blank" href="https://tools.ietf.org/html/rfc3546">TLS 服务器名称指示</a>。

本配置基于CentOS 8，且仅仅开启nginx的SNI功能。

### 1.新建用户

```bash
useradd -r -d /var/cache/nginx/ -s /sbin/nologin -U nginx
mkdir -p /var/cache/nginx/
chown -R nginx:nginx /var/cache/nginx/
```

### 2. 编译安装nginx，仅仅编译所需要的模块

```bash
cd /usr/local/src
wget https://nginx.org/download/nginx-1.19.10.tar.gz
tar -xzvf nginx-1.19.10.tar.gz
cd nginx-1.19.10
./configure --prefix=/etc/nginx --user=nginx --group=nginx --with-stream --with-stream_ssl_preread_module
make
make install
```

### 3. 测试nginx是否安装成功

```bash
nginx -t
```

### 4. 创建nginx服务（已CentOS为例）

```bash
cd /lib/systemd/system/
vim nginx.service

# [Unit]
# Description=nginx
# Documentation=https://nginx.org/en/docs/
# After=network-online.target remote-fs.target nss-lookup.target
# Wants=network-online.target
# [Service]
# Type=forking
# PIDFile=/etc/nginx/logs/nginx.pid
# ExecStartPre=/etc/nginx/sbin/nginx -t -c /etc/nginx/conf/nginx.conf
# ExecStart=/etc/nginx/sbin/nginx -c /etc/nginx/conf/nginx.conf
# ExecReload=/bin/kill -s HUP $MAINPID
# ExecStop=/bin/kill -s TERM $MAINPID
# [Install]
# WantedBy=multi-user.target

systemctl daemon-reload
#开机启动
systemctl enable nginx
```

### 5. nginx配置文件

```nginx
user  nginx;
worker_processes  1;

error_log  /etc/nginx/logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

pid        /etc/nginx/logs/nginx.pid;

events {
    worker_connections  1024;
}

stream {
    map $ssl_preread_server_name $backend_name {
        example.com web;
        test.example.com service1;

        default web;
    }

    upstream web {
        server 127.0.0.1:9999;
    }

    upstream service1 {
        server 127.0.0.1:9998;
    }
    
    server {
        listen 443 reuseport;
        listen [::]:443 reuseport;
        proxy_pass  $backend_name;
        ssl_preread on;
    }
}
```

### 6. 启动nginx

```bash
systemctl start nginx
```