---
title: PHP简单爬虫抓取新闻
date: 2017-11-9 16:59:27
tags:
 - PHP
 - QueryList
---

<img src="http://otbcgjn6c.bkt.clouddn.com/timg.jpg"  width = "400" alt="图片名称" align=center style="border:1px solid  #F6F6F6"/>

前段时间有写过简单Python爬虫（文章有代码）

### PHP爬虫基于QuerList
 1.我这里用的是QueryList3.0版本都是手动下载，官网是通过composer方法安装的，具体步骤不是很了解，感觉挺麻烦。
 2.QueryListV3.2.1版本下载地址:https://github.com/jae-jae/QueryList/tree/V3.2.1 这里有个坑如果你通过github克隆到本地不会是v3.2.1 而是4.0版本；需要打包下载 如下图：
 <img src="http://otbcgjn6c.bkt.clouddn.com/1510219317%281%29.png"alt="图片名称" align=center style="border:1px solid  #F6F6F6"/>
 3.下载完QueryListV3.2.1 还要下载PHPQuery，QueryList是基于PHPQuery。下载地址：https://github.com/jae-jae/phpQuery-single
 4.手动下载完成后可引入到项目中。

### 上代码

```
require 'phpQuery.php';
require 'QueryList.php';
use QL\QueryList;

```

这里使用了命名空间，这里我们已经引入了QueryList.php，QueryList.php使用了命名空间 namespace QL;如果要实例化QueryList，就要使用use QL\QueryList;
1.抓取腾讯新闻新闻标题
```
//获取标题
$rules = array(
    //采集id为one这个元素里面的纯文本内容
    'text' => array('.linkto','text'),
);

$url = 'http://news.qq.com/';
$data = QueryList::Query($url,$rules,'','UTF-8','GB2312',true)->getData(function($item) use($url){
        return $item;
});

print_r($data);

```
2.打印结果

```
array
(
    [0] => Array
        (
            [text] => 138万人通过国考审核创7年之最 119个职位无人报
        )

    [1] => Array
        (
            [text] => 俄媒：中国第3艘航母最终轮廓确定 或用电磁弹射
        )

    [2] => Array
        (
            [text] => 巴西众院弹劾总统案获通过 罗塞夫政党承认落败
        )

    [3] => Array
        (
            [text] => 10月CPI同比增长1.9% 涨幅连续9个月低于2%
        )
    ....


```