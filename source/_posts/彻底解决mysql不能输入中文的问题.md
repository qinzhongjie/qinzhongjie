---
title: 彻底解决mysql不能输入中文的问题
date: 2016-07-16 21:53:30
tags:
	Java报错系列
---
用struts2写了一个页面表单提交数据，数据库为MySQL。提交的时候出现了如下报错：
```
java.lang.RuntimeException: java.sql.SQLException: Incorrect string value: '\xE5\x90\x83\xE9\xA5\xAD...' for column 'hobby' at row 1 Query: insert into students (username,password,gender,hobby,birthday,email,grade) values (?,?,?,?,?,?,?) Parameters: [Ttt, ttt, male, 吃饭,睡觉, null, , 0]
	at com.itheima.dao.impl.StudentDaoImpl.save(StudentDaoImpl.java:21)
	at com.itheima.service.impl.BusinessServiceImpl.registStudent(BusinessServiceImpl.java:11)
	......
```
当把表单内容全部修改为字母时，提交成功。
然后在mysql中`\s`，查看到如下信息：

<!-- more -->

```
Connection id:          2
Current database:
Current user:           root@localhost
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.11 MySQL Community Server (GPL)
Protocol version:       10
Connection:             localhost via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 6 min 34 sec
```

根据报错查找到原因：mysql编码问题。
最终解决办法：
找到mysql配置文件my.ini，在`[mysqld]`中添加如下语句：
```
character-set-server = utf8
```
继续，找到`[mysql]`，添加如下语句：
```
default-character-set = utf8
```

原因解释：
数据库的字符集是什么，表的字符集就是什么，同样MySQL服务器有自己的字符集，他们的优先级从大到小是这样的，MySQL服务器>数据库>表，意思就是，如果不指定数据库的字符集，在创建数据库的时候它会与MySQL服务器的字符集保持一致。
通过`\s`查看msql服务器的基本信息，注意以下语句：

```
Server characterset:    utf8       //MySQL服务器字符集
Db     characterset:    utf8		//数据库字符集
Client characterset:    utf8	//客户端字符集
Conn.  characterset:    utf8	//客户端连接字符集
```

通过`show create database test`查看数据库的字符集，通过`show create table user`查看表的字符集。

如果在mysql未正确指定字符集的情况下已经创建了某个表，然后又修改了mysql服务器的字符集，存入的数据将会乱码，解决办法是修改此表的字符集和mysql服务器的一致，即utf8，通过以下命令修改

```
ALTER TABLE tbl_name CONVERT TO CHARACTER SET charset_name; 
```
tbl_name：表名
charset_name：字符集名


只要遵循客户端字符集与数据库字符集统一即可解决乱码或者无法输入中文的问题。设置mysql服务器的字符集为utf8，jdbc连接mysql的时候发送字符集为utf-8，客户端show的时候也为utf-8，就不会出现乱码问题了。

