---
title: setTimeout()的使用方法
date: 2017-7-27 21:26:27
tags:
	- jQery
	- PHP
---

### 定义:
<font color="#FF4081">setTimeout()方法在很多文档中是说 "用于在指定的毫秒数后调用函数或计算表达式",比较含糊;其实就是规定在一段时间内,调用一个函数进行延时操作;比如从一个页面2秒后跳转到另一个页面;</font>

### 用法:

<font color="#FF4081">我这有个ajax方法:</font>
```
 //要跳转的页面地址
 var url = "<?=site_url("smallshop/shopcart/dosave?key={$key}&cmid={$cmid}")?>";
   $.post(url,dt,function(data){
		  if (data.status == 0){//表示请求成功,返回成功状态
		      //成功后利用layer弹窗插件进行提示说明
			  layer.open({content: data.info,skin: 'msg',time: 2 });
			  //根据倒计时函数在两秒后跳转到指定的页面
			  setTimeout(function () {
			  	window.location.href = '<?=site_url("smallshop/channel/index?key={$key}&cmid={$cmid}")?>';
			  },2000);
		  }else{//表示请求失败,并提示失败信息
			  layer.open({content: data.info,skin: 'msg',time: 2 });
		  }
	  },'json');

```
### 总结:

<font color="#FF4081"> setTimeout() 通常是与 function 一起使用</font>
