---
title: 安装ubuntu后需要做的事
date: 2017-01-06 16:40:27
tags: [Ubuntu、web开发]
categories: Ubuntu
---

### 1.安装Vim

	sudo apt-get install vim

<!--more-->

### 2.更新源

> 系统自带的有些源在国内访问不了，能访问的速度也很慢，所以我们跟换为国内源，国内有很多不错的源，比如阿里源、163源、北京交大、上海交通、清华大学等。

+ 首先备份一下系统自带源，以备以后用到
  	sudo cp /etc/apt/sources.list  /etc/apt/sources.list.backup

+ 打开并删除源设置文件内容

      sudo gedit /etc/apt/sources.list

+ 将国内源添加到配置文件，同步更新资源包

	  apt-get update                   //更新软件源
	  apt-get upgrade                 //升级已安装的所有软件包

**阿里源：**

>deb-src http://archive.ubuntu.com/ubuntu xenial main restricted #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted multiverse universe #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted multiverse universe #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
deb http://mirrors.aliyun.com/ubuntu/ xenial multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse #Added by software-properties
deb http://archive.canonical.com/ubuntu xenial partner
deb-src http://archive.canonical.com/ubuntu xenial partner
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted multiverse universe #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-security multiverse

### 3.双系统时间修正

> Ubuntu和Windows默认的时间管理方式不同，所以双系统发生时间错乱是正常的。Ubuntu默认时间是把BIOS时间当成GMT+0时间，也就是世界标准时，而我国在东八区(GMT+8)，所以如果你的Ubuntu位置是中国的话你系统显示的时间就是BIOS时间+8小时。假如现在是早上8点，那么你Ubuntu会显示8点，这时BIOS中的时间是0点。

+ ubuntu16.04以上版本

	  sudo vim /etc/default/rcS   //将UTC=yes设为UTC=no。

+ ubuntu16.4版本

	  timedatectl set-local-rtc 1 --adjust-system-clock  //关闭UTC并重启
      timedatectl set-ntp 0

**延伸阅读：**开启win time服务
同时按下“win键”+“x”组合键，输入“services.msc”,进入“服务项”列表，找到“Windows time ”服务，双击打开,进入服务项属性对话框，点击下方“启动”选项，然后将其启动类型更改为“自动”点击确定,重启生效。

### 4.win+ubuntu 双系统修改启动顺序

+ 执行`sudo gedit /etc/defaule/grub`编辑grub配置文件，修改GRUB_DEFAULT项,GRUB_DEFAULT代表的就是启动项的顺序，从数字0开始，依次代表如下启动项，（我的电脑为win启动项为2，所以改成 GRUB_DEFAULT=2）。

+ 执行`sudo update-grub`，更新grub，重启电脑生效。


**延伸阅读**

+ 在win系统下安装ubuntu系统后默认启动的是ubuntu系统，说到启动就不得不说GRUB，Linux下大名鼎鼎的启动管理工具，当然现在已经是GRUB2了，GRUB2和GRUB最重要的区别就是，GRUB存放系统启动信息的文为/boot/grub/menu.lst，而GRUB2则为/boot/grub /grub.cfg。

+ ~~/boot/grub/grub.cfg~~ 这个文件是根据/etc/grub.d的模板和/etc/default/grub的设置自动生成的，不要修改这个文件。

### 5.安装经典菜单指示器

	sudo apt-get update
	sudo apt-get install classicmenu-indicator

**延伸阅读**
通过`sudo add-apt-repository ppa: xxx/ppa`命令在source.list里添加 ppa 源了（同时完成导入key），++add-apt-repository++是由 **Python-software-properties**这个工具包提供的,所以要先安装python-software-properties 才能使用 add-apt-repository,
安装命令：`apt-get install python-software-properties`。

### 6.Firefox浏览器设置中文

**检查修改方法分以下几种**

1.打开浏览器输入**about:config**将**general.useragent.locale**改为"zh-CN"，重启浏览器生效。

2.执行`sudo apt-get install firefox-locale-zh-hans`命令安装火狐中文包，重启生效。

3.查看是否安装ubuntu中文语言包，选择System->Administration->Language Support(系统设置>全部设置>语言支持)，系统会自动加载所需语言文件，选择安装Chinese(Simplified)，安装升级完成后将汉语(中国)移至最上边，点击应用到整个系统，重启生效。

**延伸阅读：安装Adobe Flash player插件**
+ [官网](https://get.adobe.com/flashplayer)下载，这里选择tar.gz for liunx版本下载。
+ 执行`sudo tar -zxvf flash_player_npapi_linux.x86_64.tar.gz`进行解压。
+ 执行`cd flash_player_npapi_linux.x86_64`命令进入解压后文件夹。
+ 执行`sudo cp libflashplayer.so /usr/lib/firefox/browser/plugins`,拷贝到firefox插件目录下。

### 7.安装Terminator

> Ubuntu 中默认使用的 shell 终端工具是 gnome-terminal，虽然它已经很好用了，但有时还是无法满足我们程序员各种各样的需求，Terminator可以完美地实现了在 Ubuntu在同一窗口中启动多个终端，并且可以自由的在一个窗口中分割区域建立新终端，还可以通过鼠标拉伸调整每个终端的大小。

	sudo apt-get install terminator

**延伸阅读：设置键盘快捷键**
+ 系统设置--文本输入--键盘设置--自定义快捷键--点击+号增加自定义快捷键。
+ 填写名称和命令(名称随便填写，命令填写terminator)。


### 8.安装有道词典

[官网](http://cidian.youdao.com/multi.html?vendor=fanyiweb)下载相应deb包可直接安装既可。

注：Ubuntu 16.04因为有些依赖问题就无法安装成功，因为官方的deb包（Ubuntu版本的）依赖gstreamer0.10-plugins-ugly，但是该软件在16.04里面已经没有了。

**解决办法**
1.下载deepin的包可以正常安装（亲测可用）。
2.去掉deb包里面对于该库的依赖

+ 从官网下载Ubuntu版本的deb包。
+ 创建youdao-dict目录，把该deb包解压到youdao-dict目录。`dpkg -X ./youdao-dict_1.1.0-0-ubuntu_amd64.deb  youdao-dict`
+ 解压deb包中的control信息（包的依赖就写在这个文件里面）`dpkg -e ./youdao-dict_1.1.0-0-ubuntu_amd64.deb youdao/DEBIAN`
+ 编辑control文件，删除Depends里面的gstreamer0.10-plugins-ugly。
+ 重新打包`dpkg-deb -b youdao youdaobuild.deb`
+ 安装重新打包的安装包`dpkg -i youdaobuild.deb`

### 9.安装wps
[官网](http://wps-community.org/)下载相应版本wps安装即可，安装方法多种可选，建议直接下载deb包，安装简单方便。

### 10.安装haroopad
[官网](http://pad.haroopress.com/)下载相应版本安装即可，安装方法多种可选，建议直接下载deb包，安装简单方便。

**延伸阅读：**Ubuntu的16.04是第一个版本，包括新更换的软件应用程序，GNOME软件，它已经有一个错误。 目前，在Ubuntu 16.04，它不可能安装使用软件应用的第三方应用程序,
如Ubuntu是16.04请使用dpkg命令进行安装。

### 11.解决无声音问题

1.输入下面命令安装pavucontrol：

	sudo apt install pavucontrol   //安装
	pavucontrol        //打开

2.打开pavucontrol的窗口，切换到Configuration选项卡，把show后面选择All Output Devices，Port后面选择Headphones(unplugged),声音OK。

3.写入配置文件
按照上述方法设置之后解决了问题，但是需要每次开机后都要设置一次，也就是说pavucontrol并不能自动保存我们的配置，需要我们自己设置默认的选项。

查询目前使用音频输出端口

	pacmd list | grep "active port"

打开配置文件

	sudo gedit /etc/pulse/default.pa

在末尾追加查询可用音频输出端口

	set-sink-port 0 analog-output-headphones   //本机为例

重启OK。

**延伸阅读**

如果遇到多个输出端口，按照上述方法操作会无效。

判断是否多个音频输出端口

	pacmd list | grep "active port"

查看可用音频端口启动顺序

	pacmd list > a.txt  //生成配置文件
	active port: <analog-output-headphones>   //本机端口为例查找

将查找到的index顺序写入配置文件

	sudo gedit /etc/pulse/default.pa  //打开配置文件
	set-sink-port 1 analog-output-headphones  //本机index顺序为1

