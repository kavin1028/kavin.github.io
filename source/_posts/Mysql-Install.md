layout: post
title: MySql存档板安装教程
author: kavin
categories: linux
tags:
  - mysql
top: false
cover: false
date: 2019-10-28
---

下载地址：[https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/ "点击下载")

首先解压文件，创建数据存放目录，然后在解压文件中添加my.ini文件，写入以下语句：
  
[mysqld]  
// 设置3306端口  
port=3306  
// 自定义设置mysql的安装目录，即解压mysql压缩包的目录  
basedir=D:\mysql-5.7.27-winx64  
// 自定义设置mysql数据库的数据存放目录  
datadir=D:\MySQL-Data  
// 允许最大连接数  
max_connections=200  
// 允许连接失败的次数，这是为了防止有人从该主机试图攻击数据库系统  
max_connect_errors=10  
// 服务端使用的字符集默认为UTF8  
character-set-server=utf8  
// 创建新表时将使用的默认存储引擎  
default-storage-engine=INNODB  
// 默认使用“mysql_native_password”插件认证  
default_authentication_plugin=mysql_native_password  
[mysql]  
// 设置mysql客户端默认字符集  
default-character-set=utf8  
[client]  
// 设置mysql客户端连接服务端时默认使用的端口和默认字符集  
port=3306  
default-character-set=utf8  

以管理员角色打开CMD窗口，至解压文件D:\mysql-5.7.27-winx64\bin 目录下；  
顺序执行以下命令：  
mysqld --remove		//删除  
mysqld --initialize-insecure		//初始化  
mysqld --install		//安装  
net start mysql		//启动  
mysql -uroot -p		//登陆  
注：最新版密码为root  
修改密码：alter user 'root'@'localhost' identified by 'root';
