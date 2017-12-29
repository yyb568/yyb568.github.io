---
title: 如何获取免费天气预报
date: 2017-7-20 15:17:01
tags:
 - jQery
 - PHP
 - API
---
<img src="http://otbcgjn6c.bkt.clouddn.com/3d4c72a795743e3d447d90275d322219979b1dab2438c-v0OcGi_fw658.jpg"  width = "400" alt="图片名称" align=center style="border:1px solid  #F6F6F6"/>


### Demo Github地址:
https://github.com/yyb568/WeatherDemo
### 了解
如何在本地获取免费的天气预报关键在于要有免费的天气预报接口;貌似网上还挺多的下面的是我调用的api接口地址:
http://www.sojson.com/open/api/weather/json.shtml?city=北京

### Demo测试
下面是一段简单的下拉选择框
```
<body>
    <select id="weather" name="weather">
		<option>请选择</option>
		<option value="济南">济南</option>
		<option value="泰安">泰安</option>
		<option value="潍坊">潍坊</option>
		<option value="临沂">临沂</option>
		<option value="新泰">新泰</option>
		<option value="威海">威海</option>
		<option value="长春">长春</option>
		<option value="三亚">三亚</option>
		<option value="北京">北京</option>
		<option value="上海">上海</option>
	</select><br><br>
    <div id="box">
      <ul id="con"></ul>
    </div>
</body>
```
效果图:
![](http://otbcgjn6c.bkt.clouddn.com/20170731104139.png)

### Ajax请求
1.首先要引入一个jQ框架

```
<script src="./jquery-2.1.4.js"></script>

```
2.当我选择某一个城市后,会触发一个点击事件;

```
//获取选中的城市
$("#weather").change(function(){
	var checkValue=$("#weather").val();
	var url = "./weather.php";
	$.post(url,{weather:checkValue},function(res){

	},'json')

});

```
3.当我选中后会获取相应的城市名称如:新泰,Ajax会把这个城市名称通过POST请求传到当前文件下的weather.php

### PHP文件处理请求
1.获取城市名称;
```
$city = $_POST['weather'];

```
2.PHP 将接收到城市进行组合,并以url链接形式去请求访问该API链接;以下是CURL的用法;

```
$city = $_POST['weather'];
 //初始化  
 $curl = curl_init();  
 //设置抓取的url  
 curl_setopt($curl, CURLOPT_URL, 'http://www.sojson.com/open/api/weather/json.shtml?city='.$city);
 //设置获取的信息以文件流的形式返回，而不是直接输出。  
 curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);  
 //执行命令  
 $data = curl_exec($curl);  
 //关闭URL请求  
 curl_close($curl);

```

3.最终将获取到的数据通过JSON格式并返回给请求页面

```
$city = $_POST['weather'];
 //初始化  
 $curl = curl_init();  
 //设置抓取的url  
 curl_setopt($curl, CURLOPT_URL, 'http://www.sojson.com/open/api/weather/json.shtml?city='.$city);
 //设置获取的信息以文件流的形式返回，而不是直接输出。  
 curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);  
 //执行命令  
 $data = curl_exec($curl);  
 //关闭URL请求  
 curl_close($curl);  
 //显示获得的数据  
$contents = json_decode($data, true);
if (!empty($contents)){
	$array = array('status' => 0,'info' => $contents['data']['forecast']);
	echo json_encode($array);
}

```

### 当PHP页面请求成功,并获取到数据以后,会返回成功状态,和数据给请求页面.
1.请求页获取到数据以后判断是否返回成功,如果成功表示 res.status == 0,将数据通过遍历展现在页面上;

```
if (res.status == 0){
	var con = '';
	 $.each(res.info, function(i, j){
	 	 con += "<li>日期："+j.date+"</li>";
         con += "<li>最高温："+j.high+"</li>";
         con += "<li>风："+j.fengli+"</li>";
         con += "<li>最低温："+j.low+"</li>";
    });
	$("#con").html(con);
}

```

2.根据选择不同的城市,最终显示如下结果:

![](http://otbcgjn6c.bkt.clouddn.com/150147099734.jpg)
