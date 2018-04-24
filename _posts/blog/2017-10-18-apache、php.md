---
layout: post
title: apache和php整合
category: blog
---
Centos 6.5环境

1.首先安装Apache2
yum -y install httpd
Apache安装完成后手动启动Apache2
/etc/init.d/httpd start

/etc/httpd/conf/httpd.conf:最主要的配置文件，不过很多其他的distribution都将这个文件拆成数个小文件，分别管理不同的参数。但是最主要配置文件还是以这个文件名为主。

/etc/httpd/conf.d/*.conf:这个事CentOS的特色之一，如果你不想修改原始配置文件httpd.conf的话，那么可以将你自己的额外参数独立出来，而启动apache时，这个文件就会被读入到主要配置文件。

/etc/httpd/conf.d/ssl.conf SSL相关配置，需要yum install mod_ssl 模块

/usr/lib/httpd/modules:apache支持很多的模块，所以您想要使用的模块默认都放置在此目录

/var/www/html:这里是CentOS默认的“首页”所在目录。

/var/www/error:如果因为主机设置错误，或者是浏览器端要求的数据错误，在浏览器上出现的错误信息就已这个目录的默认信息为主。

/var/www/icons:提供apache的一些小图标

/var/www/cgi-bin :默认给一些可执行的CGI程序放置的目录

/var/log/httpd:默认apache的日志文件都放在这里，对于流量大的网站来说，这个目录要很小心，因为这个文件很容易变的很大，您需要足够的空间哦

/usr/sbin/apachectl:这是Apache的主要执行文件，这个执行文件其实是shell script,它可以主动检测系统上的一些设置值，好让您启动Apache时更简单

/usr/sbin/httpd:这是主要的apache的二进制文件

/usr/bin/htpasswd:当您想登陆某些网页时，需要输入账号与密码。那么Apache本身就提供一个最基本的密码保护方式。该密码的产生就是通过这个命令实现的

2.安装MySQL
yum -y install mysql mysql-server  <br>
完成后使用如下命令启动MySQL服务  <br>
/etc/init.d/mysqld start

2.1 设置mysql密码
<br> `mysql>; USE mysql;
<br>mysql>; UPDATE user SET Password=PASSWORD(‘newpassword’) WHERE user=’root’;
<br>mysql>; FLUSH PRIVILEGES;`

3.安装php5
yum install php  <br>
安装完php5后必须要重新启动Apache以使php生效:   <br>
/etc/init.d/httpd restart

这时Apache已经可以解析执行php脚本了。由于Apache的默认网站根目录位于
/var/www/html/ 因此在此目录建立一个info.php用来测试Apache+PHP的正确安装与否:    <br>
Vi /var/www/html/info.php

Php /var/www/html/info.php //看是否测试成功
PHP与Apache已经正确安装。

4.接下来安装MySQL数据库与其它模块，如GD图形库、mbstring库等。<br>
yum -y install php-mysql php-gd php-imap php-ldap php-odbc php-pear php-xml php-xmlrpc  <br>
安装过程可能比较慢请耐心等待。完成后再次重启Apache:    <br>
/etc/init.d/httpd restart   <br>
重新在浏览器中打开IP/info.php页面应该能找到MySQL、GD、mbstring等模块
此时LAMP运行环境已经初步安装完毕。最后还需要将LAMP组件设置为自动启动

4.1设置开机启动 <br>
chkconfig –levels 2345 httpd on
<br>chkconfig –levels 2345 mysqld on

Windows环境

apache:

把svrRoot这行修改为 svrRoot “D:\Apache24″，

把DocumentRoot按照下面的内容修改：

DocumentRoot “d:/Apache24/htdocs”

<Directory “d:/Apache24/htdocs”>

把Listen Port修改为：Listen 8080

LoadModule php5_module c:/php/php5apache2_4.dll

PHPIniDir “c:/php”

AddType application/x-httpd-php .php .phtml

保存httpd.conf, 重启Apache服务。

小技巧：d:\apache24\bin\httpd.exe -k install, 这句可以把apache添加到系统服务里去。

php:

extesion_dir=“c:/php/ext”
