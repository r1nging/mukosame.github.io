---
layout: post
title: WampServer多站点配置
category: blog
---
其实网上的配置hosts文件很麻烦。

我想到个更改端口的。

C:\wamp\bin\apache\apache2.4.23\conf\extra 打开httpd-vhosts.conf

复制粘帖然后再更改成：

<VirtualHost *:8080>
	ServerName localhost
	ServerAlias localhost
	DocumentRoot c:/wamp/www2
	<Directory  "c:/wamp/www2/">
		Options +Indexes +Includes +FollowSymLinks +MultiViews
		AllowOverride All
		Require local
	</Directory>
</VirtualHost>
改3个地方，把端口改成8080，2个目录改成www2，当然，你要先去创建。

回到 C:\wamp\bin\apache\apache2.4.23\conf 打开httpd.conf

确保Require all denied被注释

<Directory />
    AllowOverride none
#   Require all denied
</Directory>
确保Include conf/extra/httpd-vhosts.conf没被注释。

# Virtual hosts
Include conf/extra/httpd-vhosts.conf
最后一步添加 Listen 0.0.0.0:8080 就配置完成了。

站点目录c:/wamp/www2

站点地址：localhost:8080

WampServer默认是空密码，进入mysql或者PhpMyAdmin执行：

set password for root@localhost = password(‘123’);
创建数据库
create database chuncai;
导入数据库：
use chuncai
source d:/chuncai.sql