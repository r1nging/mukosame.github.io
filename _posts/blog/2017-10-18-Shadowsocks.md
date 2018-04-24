---
layout: post
title: Shadowsocks科学上网
category: blog
---
安装ss，首先需要python2和pip或者easy_install套件，python3大概不行吧。

centos7自带Python 2.7.5，centos6自带python 2.6.6.但是他们都没有pip

像centos这类衍生出来的发行版，他们的源有时候内容更新的比较滞后，或者说有时候一些扩展的源根本就没有，比如pip

因此为了能够安装pip，需要先安装扩展源EPEL。

EPEL(http://fedoraproject.org/wiki/EPEL) 是由 Fedora 社区打造，为 RHEL 及衍生发行版如 CentOS、Scientific Linux 等提供高质量软件包的项目。

yum -y install epel-release

然后安装python-pip

yum -y install python-pip

pip install –upgrade pip

安装完之后别忘了清除一下cache

sudo yum clean all

安装完pip后，就可以用pip安装shadwosocks套件。

pip install shadowsocks

config.json

```{
“server”:”server IP”,
“local_address”: “127.0.0.1”,
“local_port”:1080,
“port_password”: {
“8381”: “foobar1q”,
“8382”: “foobar2w”,
“8383”: “foobar3e”,
“8384”: “foobar4r”
},
“timeout”:300,
“method”:”rc4-md5″,
“fast_open”: false
}```

网上说用rc4-md5会更快一点。

如果没有安装更新gcc，运行shadowsocks的时候会报类似以下错误：

Traceback (most recent call last):
File “/usr/bin/ssserver”, line 9, in <module>
load_entry_point(‘shadowsocks==2.4.3’, ‘console_scripts’, ‘ssserver’)()
File “/usr/lib/python2.6/site-packages/shadowsocks/server.py”, line 67, in main
tcp_servers.append(tcprelay.TCPRelay(a_config, dns_resolver, False))
File “/usr/lib/python2.6/site-packages/shadowsocks/tcprelay.py”, line 525, in __init__
server_socket.bind(sa)
File “<string>”, line 1, in bind
socket.error: [Errno 98] Address already in use

这时候yum install -y gcc 就行了。

配置完正常运行shadowsocks

ssserver -d start

问题又来了，打开客户端发现连不上，看日志发现总是time out。ping服务器是可以ping通的，首先想到的是防火墙selinux和iptables，centos7是不带selinux的。

于是

[root@195776 ~]# iptables -L
Chain INPUT (policy ACCEPT)
target prot opt source destination
ACCEPT all — anywhere anywhere state RELATED,ESTABLISHED
ACCEPT icmp — anywhere anywhere
ACCEPT all — anywhere anywhere
ACCEPT tcp — anywhere anywhere state NEW tcp dpt:ssh
REJECT all — anywhere anywhere reject-with icmp-host-prohibited

Chain FORWARD (policy ACCEPT)
target prot opt source destination
REJECT all — anywhere anywhere reject-with icmp-host-prohibited

Chain OUTPUT (policy ACCEPT)
target prot opt source destination

清楚所有iptables规则iptables -F 之后正常连接。