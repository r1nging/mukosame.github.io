---
layout: post
title: Metasploit连接postgres和mysql
category: blog
---
一、Matasploit连接postgres

kali 2.0 已经没有metasploit 这个服务了，所以service metasploit start 的老方式不起作用。

在kali 2.0中启动带数据库支持的MSF方式如下：

#1  首先启动postgresql数据库；

root@kali:~#service postgresql start

#2  初始化MSF数据库（关键步骤！）：

root@kali:~#msfdb init

#3  运行msfconsole：

root@kali:~#msfconsole

#4  在msf中查看数据库连接状态：

Msf >db_status

二、修改postgres的password

#su  postgres

-bash-3.2$psql -U postgres

postgres=#alter user postgres with password ‘new password’;

postgres=#\q

三、Metasploit连接MySQL

Msf >db_driver

[*]Active Driver:postgresql

[*]Available:postgresql,mysql

#Active Driver: postgresql 说明现在默认的数据库是postgresql

#Available:postgresql,mysql 说明MSF支持的数据库有postgresql和mysql

#然后切换默认数据库为mysql：

Msf >db_driver mysql