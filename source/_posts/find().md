---
title: find()的用法
date: 2017-7-20 15:17:01
tags:
 - jQery
---
<img src="http://otbcgjn6c.bkt.clouddn.com/dab590448925ab0dc729a38bbfc2599cafb3dbb2157db-5AQiSw_fw658.jpg"  width = "400" alt="图片名称" align=center style="border:1px solid  #F6F6F6"/>

### find():
<font color="#F44336">find() 方法返回被选元素的后代元素,一直找到最后一个后台元素(也就是找到所有find("xxx")的元素).</font>

例如我代码里面有篇文章,$soft['content']代表文章内容(包括文字和图片):
```
<div class="col-xs-12 mt3" id="content_product" >
	<?=$soft['content'] ?>
</div>
```
在页面的上所显示内容:
![](http://otbcgjn6c.bkt.clouddn.com/2017-07-25_145115.jpg)
以上内容里面的图片很大而且不规律.然后通过浏览器F12调试可以看到有<font color="#F44336">p</font>标签和<font color="#F44336">img</font>标签;这里的<font color="#F44336">img</font>图片是没有经过处理的所以图片是原比例展示出来的,在手机页面端是很难看的;
![](http://otbcgjn6c.bkt.clouddn.com/2017-07-25_145536.jpg)

### 利用jQ find()方法解决此问题;也就是把内容里面的所有图片通过遍历时图片自适应
```
//将图片自适应
$(function(){
	$("#content_product").find("img").each(function(i,j){
		$(this).attr("width", "100%");
	});
});
```
### 现在再看页面显示效果
![](http://otbcgjn6c.bkt.clouddn.com/2017-07-25_144907.jpg)
