---
title: window下wamp开发环境如何安装redis
date: 2017-8-21 16:06:38
tags:
 - redis
---
<img src="http://otbcgjn6c.bkt.clouddn.com/diary-13.jpg"  width = "400" alt="图片名称" align=center style="border:1px solid  #F6F6F6"/>



### php安装redis扩展
1.PHP必须要安装redis扩展

2.在安装之前一定要看PHP版本信息（ps：由于我没有看，导致一直安装不成功）。查看方法在wamp/www下新建info.php文件内容如下:

```
<?php
phpinfo();

```
3.查看版本信息:
![](http://otbcgjn6c.bkt.clouddn.com/2017-08-21_161536.jpg)

4.下载redis扩展php_redis.dll和php_igbinary.dll:

http://pecl.php.net/package/redis/2.2.7/windows

![](http://otbcgjn6c.bkt.clouddn.com/2017-08-21_161921.jpg)

http://windows.php.net/downloads/pecl/releases/igbinary/1.2.1/
![](http://otbcgjn6c.bkt.clouddn.com/2017-08-21_162003.jpg)

5.下载完解压缩后，将php_redis.dll和php_igbinary.dll拷贝至php的ext目录下:
![](http://otbcgjn6c.bkt.clouddn.com/2017-08-21_162552.jpg)

6.然后修改wamp/bin/apache/apache2.4.9/bin/php.ini，在该文件中加入：

```
; php_redis
extension=php_igbinary.dll
extension=php_redis.dll

```
![](http://otbcgjn6c.bkt.clouddn.com/2017-08-21_162910.jpg)

7.重启Apache后，使用phpinfo查看扩展是否成功安装
![](http://otbcgjn6c.bkt.clouddn.com/2017-08-21_162020.jpg)

8.开启redis服务。进入redis的目录我的是在（d:/redis）开启服务
![](http://otbcgjn6c.bkt.clouddn.com/2017-08-21_165739.jpg)

9.开启成功会显示：
![](http://otbcgjn6c.bkt.clouddn.com/2017-08-21_165912.jpg)

10.新建一个redistest.php测试
```
<?php
    $redis = new Redis();
    $redis->connect('127.0.0.1',6379);
    $redis->auth('123456');
    $redis->set('test','hello redis');
    echo $redis->get('test');
?>

```
11.最后得到结果
![](http://otbcgjn6c.bkt.clouddn.com/2017-08-21_170114.jpg)
