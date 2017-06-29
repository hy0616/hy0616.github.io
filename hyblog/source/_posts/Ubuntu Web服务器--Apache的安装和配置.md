---
title: Ubuntu Web服务器--Apache的安装和配置
date: 2017-06-29 20:30:16
tags: [web开发]
categories: Ubuntu
---

### 1.命令行安装Apache

打开"终端窗口"，输入"sudo apt-get install apache2"-->回车-->输入"root用户的密码"-->回车-->输入"y"-->回车,安装完成

<!--more-->

### 2.默认的网站根目录的路径

Apache安装完成后，默认的网站根目录是"/var/www/html"，在终端窗口中输入"ls /var/www/html"-->回车-->在网站根目录下有一个"index.html"文件,在ie浏览器中输入"127.0.0.1"-->回车,就可以打开该页面。

### 3.Apache的第一个配置文件apache2.conf的路径

在终端窗口中输入"ls /etc/apache2"-->回车-->有一个"apache2.conf"的配置文件。

### 4.Apache的第二个配置文件000-default.conf的路径

在终端窗口中输入"ls /etc/apache2/sites-available"-->回车-->有一个"000-default.conf"的配置文件。

### 5.修改网站的根目录

1、在终端窗口中输入"sudo vi /etc/apache2/apache2.conf"-->回车-->找到"<Directory /var/www/>"的位置-->更改"/var/www/"为新的根目录就可以了。

2、在终端窗口中输入"sudo vi /etc/apache2/sites-available/000-default.conf"-->回车-->找到"DocumentRoot /var/www/html"的位置-->更改"/var/www/html"为新的根目录就可以了，这里我把它更改为"/var/www/"。

### 6.重启Apache

在终端窗口中输入"sudo /etc/init.d/apache2 restart"-->回车-->"输入root用户密码"-->回车-->重启成功。