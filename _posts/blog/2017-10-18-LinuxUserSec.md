---
layout: post
title: Linux帐号安全
category: blog
---
黑客配置这种帐号：
email:x:43:43::/bin/email:/sbin/nologin
我们用grep bash /etc/passwd 是查找不出来的。

那么我们就和之前备份的passwd文件对比
diff /etc/passwd /root/passwd
或者
md5sum /etc/passwd /root/passwd

为了安全起见，我们把不常见的系统用户删除，比如bin,games。
分辨不出用户名，就看密码文件/etc/shadow 系统用户是空密码没有被加密过，所有有很长加密的就是设置过密码的。

或者我们干脆锁定帐号文件：
chattr +i /etc/passwd /etc/shadow
lsattr /etc/passwd /etc/shadow

关闭空密码登录，在/etc/ssh/sshd_config下设置PermitEmptyPasswords为no。