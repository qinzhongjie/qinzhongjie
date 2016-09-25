---
title: 解决每次向github提交要输入用户名和密码问题
date: 2016-05-24 10:19:23
tags:
	Git
---
通过SSH文件的验证方式可以解决每次向github提交都要输入用户名和密码的问题

检查是否存在SSH keys
在生成你的SSH key之前，先检查你的电脑上是否存在SSH keys

```
ls -al ~/.ssh
```
如果检测结果是没有，可在后续步骤中生成
如果检测结果是有，可直接用于Github配置

生成新的SSH keys 并且添加到ssh-agent中

生成新的SSH keys 

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

<!--more-->

出现选择文件路径，用默认路径就可以，按回车

```
Enter a file in which to save the key (/Users/you/.ssh/id_rsa):
```
输入密码时一般没必要输入，直接回车

```
Enter passphrase (empty for no passphrase):
```
重复输入时继续按回车

添加SSH keys到ssh-agent中
如果你使用了其他生成工具生成了新的SSH key，就需要设置此代理

```
ssh-add ~/.ssh/id_rsa
```

把SSH key 拷贝到Github网站
在电脑中找到刚生成的SSH key ，默认路径为`C:\Users\mohong\.ssh`，
用编辑器打开`id_rsa.pub`文件，复制内容。

登录Github，找到`Setting--SSH and GPG keys`，点击创建新的SSH,把内容粘贴在上面，然后起个名字便于多台设备绑定时分辨出设备。

测试SSH连接

```
ssh -T git@github.com
```
第一次使用时，你将会收到以下提示，输入`yes`即可。
```
The authenticity of host 'github.com (192.30.252.1)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)?
```

```
The authenticity of host 'github.com (192.30.252.1)' can't be established.
RSA key fingerprint is nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)?
```
最后如果看到以下内容，表示绑定成功
```
Hi username! You've successfully authenticated, but GitHub does not
provide shell access.
```


[参考资料](https://help.github.com/articles/generating-an-ssh-key/)