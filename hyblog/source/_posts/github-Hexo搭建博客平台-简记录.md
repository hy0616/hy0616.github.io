---
title: github+Hexo搭建博客平台-简记录
date: 2017-01-03 16:02:10
tags: [github pages, hexo, git]
categories: github
---

1.创建github帐号，邮箱进行认证。

2.创建username.github.io仓库，仓库名称是github特定名称。

<!--more-->

3.克隆远程仓库到本地`git clone "地址"`

4.本地仓库操作

	cd username.github.io   //进入本地仓库
    mkdir blog      //新建blog文件夹
    hexo init    //初始化hexo，生成配置文件
    npm install hexo-deployer-git --save   //下载添加hexo中git依赖插件，利用hexo上传远程仓库用到。

5.下载配置next主题[官网详细流程](http://theme-next.iissnan.com/)

6.一个分支用来存放Hexo生成的网站原始的文件，另一个分支用来存放生成的静态网页

	 git branch hexo    //创建hexo分支
     git checkout hexo   //切换到hexo分支
     git add /blog     //添加原始文件到暂存区
     git commit -m"版本注释"  //从本地暂存区提交至本地仓库hexo分支
     git push origin hexo    //将本地hexo分支提交至远程仓库

7.将github默认分支改为hexo，因为以后操作都会在hexo分支中。
8.将生成静态网页上传至master分支中。

	 hexo clean  //清理生成文件
     hexo g     //从新生成静态网页
     hexo s     //开启本地服务器，可用于本地测试
     hexo d     //上传至github