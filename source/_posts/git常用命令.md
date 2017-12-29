---
title: Git常用命令
date: 2017-12-29 22:10:14
tags:
 - GIT
---
<img src="http://otbcgjn6c.bkt.clouddn.com/u=1103434515,3403775097&fm=27&gp=0.jpg"  width = "400" alt="图片名称" align=center style="border:1px solid  #F6F6F6"/>

### git常用命令

1.从github/gitlab/码云克隆项目
```
git clone 链接地址

```
2.本地创建git版本库
```
git init
#初始化本地仓库

```
3.如何将本地代码上传到github 请看：[详细步骤](http://www.yybblog.cn/2017/07/31/%E5%A6%82%E4%BD%95%E5%B0%86%E6%9C%AC%E5%9C%B0%E4%BB%A3%E7%A0%81%E4%B8%8A%E4%BC%A0%E5%88%B0GitHub/)

4.提交本地代码到缓存区
```
git add .

git commit -m "注释"

```
5.推动到远端
```
git push origin master
```
6.创建本地分支
```
git branch 分支名称
```

7.查看分支
```
#本地分支
git branch
#远端分支
git branch -r

```
8.切换分支
```
git checkout 分支名字

```
9.git版本回退
```
git reset --hard HEAD
# 将当前版本重置为HEAD（通常用于清空缓存区,或merge失败回退）

git reset --hard HEAD^   # 回退上一个版本
git reset --hard HEAD^^  # 回退上两个版本
git reset --hard HEAD~n  # 回退上n个版本

git reset --hard <commitid>
# 回退到指定版本，commitid根据log获取

```
### svn 和 git 相比
个人更喜欢用github