---
title: stripos()的用法
date: 2017-7-20 15:17:01
tags:
 -  
 - PHP
---
这个函数经常用到,并且能快速判断,某字符串是否在另一字符串中出现,常用在条件判断中;

### 定义和用法

stripos(string,find)
参一:另一串字符
参二:要查找的字符

例子:
```
$content = 'Hello World MyBlog';
$appear = stripos($content,'my');
print_r($appear);

```
结果:
`12`

说明: 返回字符串在另一字符串中第一次出现的位置，如果没有找到字符串则返回 FALSE。

```
$content = 'Hello World MyBlog';
$appear = stripos($content,'kk');
if (stripos($content,'kk')){
	echo '存在';
}else{
	echo '不存在';
}

if (stripos($content,'lo')){
	echo '存在';
}else{
	echo '不存在';
}
```
结果分别是:
`不存在`
`存在`
