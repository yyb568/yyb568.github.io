---
title: json_decode和json_encode的使用方法
date: 2017-7-20 08:47:38
tags:
	- PHP
---
<img src="http://otbcgjn6c.bkt.clouddn.com/b7d99088a8590acb40452860b6869c9668cad7751c128-xK4ZJh_fw658.jpg"  width = "400" alt="图片名称" align=center style="border:1px solid  #F6F6F6"/>

### json_decode对json格式的字符串进行编码也就是转化成PHP变量

```
$content = $this->curl->get("http://sj.apidata.cn/?mobile={$phone}");
$contents = json_decode($content);
print_r(contents);

```
打印结果(结果是一个对象,如果要取出里面的数值,这样是不好取的):
```
stdClass Object
(
    [status] => 1
    [data] => stdClass Object
        (
            [prefix] => 131
            [province] => 山东
            [city] => 威海
            [isp] => 联通
            [code] => 631
            [zipcode] => 264200
            [types] => 中国联通 GSM
            [mobile] => 13181891701
        )

    [message] => success
)
```
<font color="#2FA3F6">当json_decode($contents,true)时会直接打印出PHP数组.</font>


```
$content = $this->curl->get("http://sj.apidata.cn/?mobile={$phone}");
$contents = json_decode($content,true);
print_r($contents);

```

<font color="#2FA3F6">打印结果 PHP数组:</font>

```
Array
(
    [status] => 1
    [data] => Array
        (
            [prefix] => 131
            [province] => 山东
            [city] => 威海
            [isp] => 联通
            [code] => 631
            [zipcode] => 264200
            [types] => 中国联通 GSM
            [mobile] => 13181891701
        )

    [message] => success
)

```
<font color="#FF4081">可以看出 json_decode($contents,true)输出的一个关联数组,由此可知json_decode($contents）输出的是对象,而json_decode("$contents",true)是把它强制生成PHP关联数组</font>

### json_decode 对PHP变量进行 JSON 编码

```
<?php
$arr = array ('a'=>1,'b'=>2,'c'=>3,'d'=>4,'e'=>5);

echo json_encode($arr);
?>
```
<font color="#2FA3F6">打印结果 PHP数组:</font>
```
{"a":1,"b":2,"c":3,"d":4,"e":5}

```
### 最后:

可以看出json_encode()和json_decode()是编译和反编译过程，注意json只接受utf-8编码的字符，所以json_encode()的参数必须是utf-8编码，否则会得到空字符或者null。
