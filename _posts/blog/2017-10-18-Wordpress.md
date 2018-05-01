---
layout: post
title: Centos7安装wordpress的一些问题
category: blog
---
1.安装MariaDB

CentOS 7.0中，已经使用MariaDB替代了MySQL数据库

`rpm -qa | grep MariaDB`

看看本机又没安装MariaDB,没有的话安装

yum install mariadb mariadb-server

systemctl start mariadb.service #启动MariaDB

systemctl enable mariadb.service #设置开机启动

mysql_secure_installation #启动MariaDB并设置密码

systemctl restart mariadb.service #重启MariaDB

mysqladmin -u root -p create wordpress #创建Wordpress数据库

2.安装PHP

```yum install php
yum install php-mysql php-gd libjpeg* php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-bcmath php-mhash #安装php组件
systemctl restart mariadb.service #重启MariaDB
systemctl restart httpd.service #重启apache

```

请输入您的FTP登录凭据以继续：
http://www.itbulu.com/wordpress-ftp.html

MariaDB基本操作：
http://blog.csdn.NET/wwb456/article/details/53559564

centos7安装lamp:
http://www.jb51.Net/os/188488.html

MariaDB 的简单配置：
http://www.linuxidc.com/Linux/2016-03/128880.htm