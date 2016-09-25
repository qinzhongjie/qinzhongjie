---
title: Linux下后台运行jar文件
date: 2016-07-04 10:34:58
tags:
	Linux
---
当我们把java程序打成jar包后，放到linux上通过putty或其它终端执行的时候，如果按照：java -jar xxxx.jar执行，当我们退出putty或终端的时候，xxxx.jar这个程序也会停止。为了保证程序能够一直运行，应该改为这样运行： `java -jar xxx.jar &`命令，则程序会在后台一直运行，值得注意的是，此时程序控制台输出会被转移到nohup.out文件中，这个nohup.out文件的位置就在jar包的当前文件夹内。
但是有时候在这一步会有问题，当把终端关闭后，进程会自动被关闭，察看nohup.out可以看到在关闭终端瞬间服务自动关闭。
有个操作终端时的细节：当shell中提示了nohup成功后还需要按终端上键盘任意键退回到shell输入命令窗口，然后通过在shell中输入`exit`来退出终端；而我是每次在nohup执行成功后直接点关闭程序按钮关闭终端。所以这时候会断掉该命令所对应的session，导致nohup对应的进程被通知需要一起shutdown。

<!--more-->

当需要关闭这个后台运行的jar文件时，执行以下命令查看目前的所有进程：
`ps -A`
找到对应的pid，然后执行以下命令杀死进程：
`kill -9 pid`
