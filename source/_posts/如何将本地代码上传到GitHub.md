---
title: 如何将本地代码上传到GitHub
date: 2017-7-31 15:35:46
tags:
 - GitHub
---

<img src="http://otbcgjn6c.bkt.clouddn.com/diary-14.jpg"  width = "400" alt="图片名称" align=center style="border:1px solid  #F6F6F6"/>



### 第一步

安装Git Bash版本控制器: https://git-for-windows.github.io/

### 第二步

安装好之后进入到你的本地项目根目录,右击鼠标点击 Git Bash Here

![](http://otbcgjn6c.bkt.clouddn.com/2017-07-31_154306.jpg)

### 第三步

执行git命令

> git init

### 第四步

将项目的所有文件添加到仓库中
如果想添加某个特定的文件，只需把.换成特定的文件名即可

> git add .

### 第五步

将add的文件commit到仓库

> git commit -m "注释语句"

### 第六步

去github上创建自己的仓库地址,如下图所示：
##### 1.点击New repository
![](http://otbcgjn6c.bkt.clouddn.com/2017-07-31_154916.jpg)
##### 2.填写好仓库信息后点击Create repository创建
![](http://otbcgjn6c.bkt.clouddn.com/2017-07-31_155434.jpg)
##### 3.如下就是所创建的仓库,红圈是克隆下载地址暂时先不用
![](http://otbcgjn6c.bkt.clouddn.com/2017-07-31_155806.jpg)
##### 4.拿到创建的仓库的https地址,也就是url地址
![](http://otbcgjn6c.bkt.clouddn.com/2017-07-31_160114.jpg)

### 第七步：重点来了，将本地的仓库关联到github上
> git remote add origin https://github.com/yyb568/WeatherDemo

### 第八步：上传github之前，要先pull一下，执行如下命令：

> git pull origin master

![](http://otbcgjn6c.bkt.clouddn.com/2017-07-31_160818.jpg)

### 第九步，也就是最后一步，上传代码到github远程仓库
> git push -u origin master
执行完后，如果没有异常，等待执行完就上传成功了，中间可能会让你输入Username和Password，你只要输入github的账号和密码就行了

### 最后GitHub成功后截图

![](http://otbcgjn6c.bkt.clouddn.com/2017-07-31_161307.jpg)
