---
title: Html+PHP实现简单计算器
date: 2018-1-9 15:48:03
tags:
 - GIT
---

```
$one = $_POST['one'];
$two = $_POST['two'];
$type = $_POST['type'];

```

### 面试经
1.如果让你写一个简单计算器（其实是很简单的，就怕临时发挥懵逼，比如我）

#### 上html代码 
1.index.html
```
<html>
    <meta http-equiv="content-Type" content="text/html; charset=utf-8">
    <title>计算器</title>
        <head></head>
        <body>
            <form>
                数字1：<input type="text" id ="one" name="one"><br>
                数字2：<input type="text" id ="two" name="two"><br><br>
                <button type="button" id="jias" onClick="jia()" data-type="1">加</button>
                <button type="button" id="jians" onClick="jian()" data-type="2">减</button>
                <button type="button" id="chengs" onClick="cheng()" data-type="3">乘</button>
                <button type="button" id="chus" onClick="chu()" data-type="4">除</button>
            </form>
            结果：<div id="res"></div>
        </body>
        <script src="./jquery.min.js"></script>
        <script>
            function jia(){
               var one = $("#one").val();
               var two = $("#two").val(); 
               var type = $("#jias").data("type");
               var url = './index.php';
               $.post(url,{'one':one,'two':two,'type':type},function(data){
                    if (data.status == 1){
                        $("#res").text(data.res);
                    }
               },'json')
            }

            function jian(){
               var one = $("#one").val();
               var two = $("#two").val(); 
               var type = $("#jians").data("type");
               var url = './index.php';
               $.post(url,{'one':one,'two':two,'type':type},function(data){
                    if (data.status == 1){
                        $("#res").text(data.res);
                    }
               },'json')
            }

            function cheng(){
               var one = $("#one").val();
               var two = $("#two").val(); 
               var type = $("#chengs").data("type");
               var url = './index.php';
               $.post(url,{'one':one,'two':two,'type':type},function(data){
                    if (data.status == 1){
                        $("#res").text(data.res);
                    }
               },'json')
            }

            function chu(){
               var one = $("#one").val();
               var two = $("#two").val(); 
               var type = $("#chus").data("type");
               var url = './index.php';
               $.post(url,{'one':one,'two':two,'type':type},function(data){
                    if (data.status == 1){
                        $("#res").text(data.res);
                    }
               },'json')
            }
        </script>
</html>

```
#### 上php代码
1.index.php
```

$one = $_POST['one'];
$two = $_POST['two'];
$type = $_POST['type'];

if ($type == 1){
	$res = $one + $two;
}else if($type == 2){
	$res = $one - $two;
}else if($type == 3){
	$res = $one * $two;
}else if($type == 4){
	if ($two == 0){
		$two = 1;
	}
	$res = $one / $two;
}

$array = array('res' => $res,'status' => 1);
echo json_encode($array);

```
#### 总结
个人素质不达标