---
layout: post
title: Python技巧笔记
category: blog
---

一、快捷键

Ctrl+z 退出命令行
Ctrl+c 退出执行过程

二、PIP
python2.7和3.6都内置了pip和easy_install，在Scripts目录下，Windows添加python环境变量的时候记得把pip目录的也加上。

python2.7的pip需要 python2 -m pip -V

pip源：

新建 C:\Users\用户名\pip\pip.ini

[global]
index-url = https://pypi.douban.com/simple
[install]
trusted-host=pypi.doubanio.com

或者：

pip install lxml –trusted-host mirrors.aliyun.com -i http://mirrors.aliyun.com/pypi/simple/

三、其它

pip -V 查看pip版本和这个pip隶属与2.7还是3.6

python -V 查看python版本

python -m SimpleHTTPServer 8080 http服务器和共享

python -h 查看帮助

Python文档：http://python.usyiyi.cn/translate/python_352/index.html

四、Jupyter notebook

Jupyter notebook的启动目录修改：

cmd：jupyter notebook --generate-config

找到：jupyter_notebook_config.py  修改：c.NotebookApp.notebook_dir 快捷方式右键去掉最后一个。