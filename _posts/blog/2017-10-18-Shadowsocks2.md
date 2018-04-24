---
layout: post
title: Shadowsocks一系列问题
category: blog
---
一

Traceback (most recent call last):
File “XXXXXXX”, line 5, in
from pkg_resources import load_entry_point
ImportError: No module named pkg_resources

升级py，参考：http://www.cnblogs.com/emanlee/p/6111613.html

二

ss日志正常，客户端日志正常，可是就是连不上？？？

修改客户端本地端口1080试试

三

访问g哥，出现http、proxy、request 等等错误？？？

看ss服务器日志。

四

cat /var/log/shadowsocks.log

Traceback (most recent call last):
File “/usr/bin/ssserver”, line 11, in
load_entry_point(‘shadowsocks==2.8.2’, ‘console_scripts’, ‘ssserver’)()
File “/usr/lib/python2.7/site-packages/shadowsocks/server.py”, line 68, in main
tcp_servers.append(tcprelay.TCPRelay(a_config, dns_resolver, False))
File “/usr/lib/python2.7/site-packages/shadowsocks/tcprelay.py”, line 582, in __init__
server_socket.bind(sa)
File “/usr/lib64/python2.7/socket.py”, line 224, in meth
return getattr(self._sock,name)(*args)
socket.error: [Errno 99] Cannot assign requested address

这个问题一般是服务器ip的问题，填错了？端口占用？或者改成0.0.0.0