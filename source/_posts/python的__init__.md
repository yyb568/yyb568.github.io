---
title: Python中的包和__init__.py文件
date: 2018-1-7 22:21:20
tags:
 - Python
---
<img src="http://otbcgjn6c.bkt.clouddn.com/timgbao.jpg"  width = "400" alt="图片名称" align=center style="border:1px solid  #F6F6F6"/>

### Python中的包
方式：
1.使用import 文件.模块 的方式导入包
2.使用from 文件夹 import 模块 的方式导入
理解：
包将有联系的模块组织在一起，放到同一个文件夹下，并且在这个文件夹下创建一个名字为__init__.py文件，那么这个夹就称之为 包

### __init__.py有什么用

1.__init__.py 控制着包的导入
2.当__init__.py 为空时：仅仅是把这个包导入，不会导入包中的模块
3.可以在这个文件中编写语句，当导入时，这些语句就会被执行

### 例子
现有如下目录
```
Phone/
    __init__.py
    common_util.py
    Voicedta/
        __init__.py
        Pots.py
        Isdn.py
    Fax/
        __init__.py
        G3.py
    Mobile/
        __init__.py
        Analog.py
        igital.py
    Pager/
        __init__.py
        Numeric.py

```
1.Phone 是最顶级的包，Voicedta、Fax等是子包，我们可以这样引入：

```
import Phone.Mobile.Analog

```
2.也可以使用from 文件夹 import 模块导入

```
from Phone import Mobile
from Phone.Molile import Analog

```
#### 在以上目录中会看到很多__init__.py文件
理解：这些是初始化模块，from-import 语句导入子包的时候需要用到它，如果没有用到，他们可以使空文件。