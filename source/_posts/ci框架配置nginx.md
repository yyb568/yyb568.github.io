---
title: Nginx的配置
date: 2017-7-20 15:17:01
tags:
 - PHP
 - Nginx
---

```
 include enable-php.conf;
 location / {
    index  index.html index.htm index.php;                                                                                                                                                                      
    rewrite ^/$ /index.php last;
    rewrite ^/(?!index\.php|robots\.txt|images|js|styles)(.*)$ /index.php/$1 last;
  }

```
<font color="red">以上代码是重点部分</font>

### 前言
1.前段时间临近双十一在阿里云9.9买了半年服务器，想着弄个网站部署在线上。之前在nginx上部署过，不过那是别人弄的。什么事都是还要靠自己，是真理。
2.为此写下步骤，以便下次部署直接来找教程。
3.为了能让CI框架在nginx上跑起来。废了我两三天时间。不过还是配置好了。

### 安装linux
1.我这里用的是lnmp一键安装包 教程地址：https://lnmp.org/

### 安装好之后
1.开始部署你的web网站，如果在本地可以运行。那直接克隆到服务器上
2.我的线上项目地址
![](http://otbcgjn6c.bkt.clouddn.com/1510737091%281%29.jpg)
3.当你以域名去范文访问的时候回出现以类似下错误，这是nginx禁止程序跨目录访问
```
Warning: require(): open_basedir restriction in effect. File(/home/wwwroot/***/bootstrap/autoload.php) is not within the allowed path(s): (/home/wwwroot/***/public/:/tmp/:/proc/) in /home/wwwroot/***/public/index.php on 

```
解决办法将 /usr/local/nginx/conf/fastcgi.conf 里面的fastcgi_param PHP_ADMIN_VALUE "open_basedir=$document_root/:/tmp/:/proc/"; 在该行行前添加 # 或删除改行，需要重启nginx。 lnmp nginx reload

4.以上弄好以后，继续访问线上ip地址。可能会出现404，特别是ci框架里面的site_url()方法和redirect()方法。

### 重点介绍
1.在server项里面：nginx引入了月一个 文件 include enable-php.conf;这个文件里面就包含了，解析php，运行php文件。我配置如下

```
location ~ [^/]\.php(/|$)
{                                                                     
   try_files $uri =404;
   fastcgi_pass  unix:/tmp/php-cgi.sock;
   fastcgi_param PATH_INFO $fastcgi_path_info;
   if ($uri ~ "^(.+?\.php)(/.*)$") {
           set $script     $1;
           set $path_info  $2;
       }   
  fastcgi_split_path_info ^(.+\.php)(.*)$;
  fastcgi_index index.php;
  include fastcgi.conf;
}
```
在原来基础上加了这几段代码
```
fastcgi_param PATH_INFO $fastcgi_path_info;
   if ($uri ~ "^(.+?\.php)(/.*)$") {
           set $script     $1;
           set $path_info  $2;
       }   
  fastcgi_split_path_info ^(.+\.php)(.*)$;
```
以上是enable-php.conf文件配置

3.在你的框架中可能会有redirect()方法,我的一只是404错误，原因就是这个,后来在server包含中 include enable-php.conf下行添加如下代码
```
location / {
    index  index.html index.htm index.php;                                                 
    rewrite ^/$ /index.php last;
    rewrite ^/(?!index\.php|robots\.txt|images|js|styles)(.*)$ /index.php/$1 last;
 }
```
4.在以ip地址访问成功访问到。

5.将nginx.conf代码全部贴出

```
user  www www;

worker_processes auto;

error_log  /home/wwwlogs/nginx_error.log  crit;

pid        /usr/local/nginx/logs/nginx.pid;

#Specifies the value for maximum file descriptors that can be opened by this process.
worker_rlimit_nofile 51200;

events
    {
        use epoll;
        worker_connections 51200;
        multi_accept on;
    }

http
    {
        include       mime.types;
        default_type  application/octet-stream;

        server_names_hash_bucket_size 128;
        client_header_buffer_size 32k;
        large_client_header_buffers 4 32k;
        client_max_body_size 50m;

        sendfile   on;
        tcp_nopush on;

        keepalive_timeout 60;

        tcp_nodelay on;

        fastcgi_connect_timeout 300;
        fastcgi_send_timeout 300;
        fastcgi_read_timeout 300;
        fastcgi_buffer_size 64k;
        fastcgi_buffers 4 64k;
        fastcgi_busy_buffers_size 128k;
        fastcgi_temp_file_write_size 256k;

        gzip on;
        gzip_min_length  1k;
        gzip_buffers     4 16k;
        gzip_http_version 1.1;
        gzip_comp_level 2;
        gzip_types     text/plain application/javascript application/x-javascript text/javascript text/css application/xml application/xml+rss;
        gzip_vary on;
        gzip_proxied   expired no-cache no-store private auth;
        gzip_disable   "MSIE [1-6]\.";

        #limit_conn_zone $binary_remote_addr zone=perip:10m;
        ##If enable limit_conn_zone,add "limit_conn perip 10;" to server section.

        server_tokens off;
        access_log off;

server
    {
        listen 80 default_server;
        #listen [::]:80 default_server ipv6only=on;
        server_name 106.14.117.93;
        index index.html index.htm index.php;
        root /data/www/min/www; 

        #error_page   404   /404.html;

        # Deny access to PHP files in specific directory
        #location ~ /(wp-content|uploads|wp-includes|images)/.*\.php$ { deny all; }

       include enable-php.conf;
       location / {
          index  index.html index.htm index.php;
          rewrite ^/$ /index.php last;
          rewrite ^/(?!index\.php|robots\.txt|images|js|styles)(.*)$ /index.php/$1 last;
        }
        location /nginx_status
        {
            stub_status on;
            access_log   off;
        }

        location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
        {
            expires      30d;
        }

        location ~ .*\.(js|css)?$
        {
            expires      12h;
        }

        location ~ /.well-known {
            allow all;
        }

        location ~ /\.
        {
            deny all;
        }

        access_log  /home/wwwlogs/access.log;
    }
include vhost/*.conf;
}

```