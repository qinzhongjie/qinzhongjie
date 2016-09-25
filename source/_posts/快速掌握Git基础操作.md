---
title: 快速掌握Git基础操作
date: 2015-10-17 17:31:03
tags:
	- Git
---
>常用的[Git](https://git-scm.com/)命令

<!--more-->

## **初始化配置**
`$ git config --global user.name "Your Name"`
`$ git config --global user.email "email@example.com"`



## **创建版本库**（初始化仓库）
windows系统下仓库路径不要出现中文
`$git init`


## **把文件添加到版本库**
 添加所有改动过的文件
`$git add .   `
提交到版本库
` $git commit -m "message"`


## **查看修改结果**
查看修改状态
`$git status `
查看具体修改内容`
`$git diff filename.txt`


## **版本回退**
版本历史记录
`$git log --oneline --decorate --graph`
回退到上一个版本
`$ git reset --hard HEAD^`
重返未来
`$git reflog`


## **撤销修改**
 - 未执行`$git add .`时，丢弃工作区的修改
 *当还没有提交到暂存区时，会和版本库一样*
*当提交到暂存区时，会回到添加暂存区后的状态*
	 - `$git checkout -- readme.txt`
	 - `$git checkout -- .`
 - 执行了`$git add .`，但未`commit`
 *把暂存区的修改撤销，重新放回工作区*
	 - `$git reset HEAD file.txt`
 - 执行了`commit`，
	 - 版本回退


## 删除文件
 - 从本地直接删除（此时工作区和版本库不一致）
 -     - 确实要从版本库中删除文件
		 -  `$git rm -rf test.txt`
		 -  `$git commit -m "message"`
	 - 删错了想恢复
		 - `$git checkout -- test.txt`


## 远程仓库
 - 创建SSH key
	 - 生成SSH key
		 - `$ssh-keygen -t rsa -b 4096 -C "your email@com"`
	 - 绑定在github网站
	 - 检测是否绑定成功
		 - `$ssh -T git@github.com`
	 - 添加远程库
		 - 在github上新建一个仓库，如learn.git
		 - 在本地learn.git仓库中运行下列语句来关联远程库
			 - `$git remote add origin git@github.com:qinzhongjie/learngit.git`
		 - 把本地仓库中所有内容推送到远程库
			 - 首次推送，-u为了关联两个仓库 `$git push -u origin master` 
			 - 以后的推送 `$git push origin master` 
	 - 克隆远程库
		 - `$git clone git@github.com:qinzhongjie/learngit.git`


注意： .gitignore只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。
    正确的做法是在每个clone下来的仓库中手动设置不要检查特定文件的更改情况。
    git update-index --assume-unchanged PATH    在PATH处输入要忽略的文件。

