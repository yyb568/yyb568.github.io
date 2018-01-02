---
title: PHP中array_slice()的用法
date: 2018-1-2 21:25:19
tags:
 - GIT
---
<img src="http://otbcgjn6c.bkt.clouddn.com/timgadas.jpg"  width = "400" alt="图片名称" align=center style="border:1px solid  #F6F6F6"/>

### 理解

1.个人理解：获取一个数组中任意相邻的几个元素
例如1：获取$list数组前两位数组元素

```
$list = array(
	"a" => "你",
	"b" => "好",
	"c" => "啊",
	"d" => "我",
	"e" => "是",
	"f" => "小",
	"g" => "明",
	"h" => "山东",
	"i" => "士大夫",
	"j" => "阿斯蒂芬",
	"k" => "士大夫山东",
	"l" => "发过火",
	"m" => "更好",
	"n" => "大公会",
	"o" => "sad",
	"p" => "国家",
	"q" => "任天野"
);
$slicelist = array_slice($list,0,2);
print_r($slicelist);
```

打印结果：
```
Array
(
    [a] => 你
    [b] => 好
)

```
例如2：获取$list数组第三位和第四位元素

```
$slicelist = array_slice($list,2,2);
print_r($slicelist);
```

打印结果:
```
Array
(
    [c] => 啊
    [d] => 我
)
```
例如3：获取$list数组第五位和第六位元素
```
$slicelist = array_slice($list,4,2);
print_r($slicelist);
```
打印结果:
```
Array
(
    [e] => 是
    [f] => 小
)

```

整体理解：
截取数组的相邻的几位元素，
第5位和第6位，array_slice($list,5-1,6-5+1)；
第10位和第12位，array_slice($list,10-1,12-10+1)；
第10位和第15位，array_slice($list,10-1,15-10+1)；
····
···
··