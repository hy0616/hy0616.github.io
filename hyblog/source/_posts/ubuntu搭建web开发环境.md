---
title: ubuntu搭建web开发环境
date: 2017-01-09 16:40:14
tags: [Ubuntu, web开发环境]
categories: web开发
---

### 一、安装nodejs

#####**源码安装**
1.官网下载nodejs源码，[nodejs官网](http://nodejs.org)或者[nodejs中文网](http://nodejs.cn)，下载相应版本。

<!--more-->

2.源码解压安装

    apt-get update  //更新源，近期已更新可省略
    apt-get install python gcc make g++  //安装依赖包，已安装可省略
	sudo cp -r node-v6.9.2.tar.gz /opt/nodejs  //复制源码到安装目录
    sudo tar -zxvf node-v6.9.2.tar.gz  //解压源码
    cd node-v6.9.2  //进入源码
    sudo ./configure  //检测系统配置，生成makefile文件。
    sudo make  //源码编译
    sudo make install  //安装

3.执行`node -v` 显示node版本号，安装成功。
4.安装tj大神写的n(nde版本管理工具)`sudo npm install -g n`,此后就可用n来切换、安装node版本了。

**延伸阅读:**
```
sudo n  //切换nodejs版本
sudo n latest  //安装官网最新发布版本
sudo n stable  //安装官网稳定版本
sudo n lts  //安装官网最新正式发布LTS版本
sudo n 6.9.2  //安装指定版本
sudo n rm 6.9.2 或 sudo n -6.9.2   //删除指定版本nodejs
sudo n ls  //查看可用node版本
```

### 二、通过NPM安装一系列前端管理工具

1.执行`sudo npm install -g gulp` 命令安装gulp(自动化构建工具)。
2.执行`sudo npm install -g grunt-cli` 命令安装grunt(自动化构建工具)。
3.执行`sudo npm install -g bower` 命令安装bower(前端包管理工具)。

### 三、安装Git

1.执行`sudo apt-get install git`命令安装git
2.测试git是否安装成功，执行`git --version`命令，输出版本号，安装成功。
3.配置git

	git config --global user.name "Your Name"  //指定用户名
    git config --global user.email "youremail@domain.com"  //指定邮箱
    git config --list  //查看配置信息

4.创建本地repository

    sudo git init localGit //创建名为localGit的本地仓库
    cd localGit  //进入文件夹
    touch test.md  //创建一个文件
    git add test.md  //添加至本地仓库
    git commit -m "注释"  //提交至本地仓库

5.提交远程仓库

    git remote add origin git@github.com:<github用户名>/<仓库名称>git    //本地仓库可远程仓库链接
    git push -u origin master  //提交至远程仓库，origin(仓库名)，master(指定分支)

### 四、安装Sublime Text3

1.首先添加sublime text 3的仓库

	sudo add-apt-repository ppa:webupd8team/sublime-text-3

2.更新软件库

	sudo apt-get update

3.安装Sublime Text 3

	sudo apt install sublime-text-installer

4.安装插件管理器Packeage Control

执行命令`subl`打开Sublime Text 3,按快捷键**ctrl + shift + p** 在弹出的窗口中查找**install package control**命令，单击运行.

5.解决中文输入法问题

+ 安装fcitx`sudo apt-get install fcitx-table-pinyin `
+ 配置更改为fcitx，重启电脑
+ 打补丁，github[下载地址](https://github.com/lyfeyaj/sublime-text-imfix)

      sudo apt-get update && sudo apt-get upgrade  //更新
      git clone https://github.com/lyfeyaj/sublime-text-imfix.git  //下载
      cd sublime-text-imfix  //进入
      ./sublime-imfix  //执行脚本
+ 重启Sublime生效。

### 五、安装chrome
[官网](http://www.google.cn/chrome/browser/desktop/index.html)下载deb包直接安装。
