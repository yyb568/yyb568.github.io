---
title: Python爬虫爬取校花网图片
date: 2017-9-13 17:20:43
tags:
 - Python
---

<img src="http://otbcgjn6c.bkt.clouddn.com/timg.jpg"  width = "400" alt="图片名称" align=center style="border:1px solid  #F6F6F6"/>



基于Python3.5爬虫

```
import requests
import re
from bs4 import BeautifulSoup

```
1.首先要引入包
2.如有缺包请 pip install requests 等

### 直接上爬虫代码

```
import requests
import re
from bs4 import BeautifulSoup

def gethtml(num):
    header = {'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36'}
    try:
        if num == 1:
            url = 'http://www.xiaohuar.com/hua/'
        else:
            url = 'http://www.xiaohuar.com/list-1-'+str(num)+'.html'
        res = requests.get(url,headers = header,timeout=10)
        res.raise_for_status()
        res.encoding = res.apparent_encoding#转码
        print('爬取第{}页:'.format(num))
        return res.text
    except:
        print("链接异常！！！")
        return ''

def findhtml(text,ulist):
    soup = BeautifulSoup(text,'lxml')
    links = soup.find_all('div',class_='item')
    mainurl = 'http://www.xiaohuar.com'
    for link in links:
        #获取标题
        title = link.find('img')['alt']
        #获取图片链接
        imgurl = link.find('img')['src']
        #获取后缀
        zhui = imgurl[-4:]
        #拼接图片名称
        imgname = title + zhui
        print(imgname)
        #图片下载地址
        imgurlinfo = mainurl + imgurl
        img = requests.get(imgurlinfo)
        with open('./xiaohua/'+imgname,"wb") as code:
            code.write(img.content)
    
if __name__ == '__main__':
    ulist = []
    for i in range(1,5):
        text = gethtml(i)
        findhtml(text,ulist)


```
### 