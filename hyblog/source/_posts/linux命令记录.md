---
title: linux命令记录
date: 2017-03-01 16:40:14
tags: [Ubuntu]
categories: Ubuntu
---

### 1.查看端口占用情况并杀死进程

+ `ps -ef | grep 8080` 查询端口占用

+ `kill -9 端口号`  杀死进程

### 2.通过关键字查找包含内容文件

+ `find /xxx -name "*" | xargs grep "content"`

注： /xxx表示路径，"*"表示在含有某关键字名字下的文件中查找。

例： 当前目录下搜索含有Temporary_random内容的所有文件

`find ./ -name "*" | xargs grep "Temporary_random"`

### 3.安装deb命令

>deb是Debian Linux的安装格式，跟Red Hat的rpm非常相似，最基本的安装命令是：dpkg -i xxx.deb

>dpkg 是Debian Package的简写，是为Debian 专门开发的套件管理系统，方便软件的安装、更新及移除。所有源自Debian的Linux发行版都使用dpkg，例如Ubuntu、Knoppix 等。

dpkg命令常用格式如下：

+ `sudo dpkg -I xxx.deb` 查看软件包的详细信息，包括软件名称、版本以及大小等（其中-I等价于–info）

+ `sudo dpkg -c xxx.deb` 查看软件包中包含的文件结构（其中-c等价于–contents）

+ `sudo dpkg -i xxx.deb` 安装软件包（其中-i等价于–install）

+ `sudo dpkg -l xxx.deb` 查看软件包的信息（软件名称可通过dpkg -I命令查看，其中-l等价于–list）

+ `sudo dpkg -L xxx.deb` 查看软件包安装的所有文件（软件名称可通过dpkg -I命令查看，其中-L等价于–listfiles）

+ `sudo dpkg -s xxx.deb` 查看软件包的详细信息（软件名称可通过dpkg -I命令查看，其中-s等价于–status）

+ `sudo dpkg -r xxx.deb` 卸载软件包（软件名称可通过dpkg -I命令查看，其中-r等价于–remove）

注： dpkg命令无法自动解决依赖关系。如果安装的deb包存在依赖包，则应避免使用此命令，或者按照依赖关系顺序安装依赖包。