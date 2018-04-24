---
layout: post
title: Metasploit Nessus、Nexpose笔记
category: blog
---
在MSF里用这两款强大的漏洞扫描工具。

启动MSF请看上一篇文章.

一、Nessus

使用Nessus 扫描完成后生成.nessus 格式的报告，导入到MSF：

db_connect postgres:toor@127.0.0.1/msf

db_import /tmp/nessus_report_Host_test.nessus

db_hosts –c address,svcs,vulns

db_vulns

在MSF 中使用Nessus：

db_connect postgres:toor@127.0.0.1/msf

load nessus

nessus_connect nessus:toor@192.168.1.111:8834 ok

nessus_policy_list #查看存在的扫描规则

nessus_scan_new 2 bridge_scan 192.168.1.111 #2 表示规则的ID 号，bridge_scan 自定义扫

描名称

nessus_scan_status #查看扫描进行状态

nessus_report_list #查看扫描结果

nessus_report_get skjla243-3b5d-******* #导入报告

db_hosts –c address,svcs,vulns

二、NeXpose

在nexpose 中扫描目标并生成xml 格式的报告后，将报告导入到msf：

db_connect postgres:toor@127.0.0.1/msf

db_import /tmp/host_test.xml

db_hosts –c address,svvs,vulns

db_vulns

在MSF 中运行nexpose：

db_destroy postgres:toor@127.0.0.l1/msf

db_connect postgres:toor@127.0.0.1/msf

load nexpose

nexpose_connect –h

nexpose_connect nexpose:toor@192.168.1.111 ok

nexpose_scan 192.168.1.195

db_hosts –c address