---
title: MySQL基础
date: 2016-04-26 11:21:16
tags:
	MySQL
---

# SQL简介
Structured Query Language 结构化查询语言
关系型数据库
由标准和扩展部分组成

# SQL语句的组成
- DQL 数据查询语言
- DML 数据操作语言
- DDL 数据定义语言
- DCL 数据控制语言
- TPL 事务处理语言
- CCL 指针控制语言

<!--more-->

# 常用数据库
- Oracle
- DB2
- MySQL

# MySQL的安装与配置
大小写问题：mysql在windows系统中不区分大小写，但在其他系统中严格区分大小写。
验证是否安装配置成功：
`mysql -u root -p`

（Hibernate）
Java类和表结构对应的
Java对象和表中的一条记录是对应的

# DDL：数据定义语言
作用：用于描述数据库中要存储的现实世界实体的语言。即创建数据库和表的结构
常用关键字：`CREATE` , `ALTER` , `DROP` , `TRUNCATE`

## 库操作
显示所有的数据库：
`show databases;`

创建一个名为mydb1的数据库：
`create database mydb1;`

查看数据库的创建细节，可以看到使用的字符集
`show create database mydb1;`

创建一个使用gbk字符集的mydb2数据库：
`create database mydb2 character set gbk;`

删除前面创建的mydb2数据库：
`drop database mydb2;`

把mydb1的字符集修改为utf8;
`alter database mydb1 character set utf8;`

## 表操作
选择数据库
`use mydb1;`

显示当前选择的数据库
`select database();`

创建一个员工表：
```
create table employee(
	id int,
	name varchar(100),
	gender varchar(10),
	birthday date,
	job varchar(100),
	salary float(8,2),
	resume text
);
```

查看库中的所有表格
`show tables;`

查看表的结构
`desc employee;`

查看表的创建细节
`show create table employee;`

添加一个image列
`alter table employee add image blob;`

修改job列的长度为60
`alter table employee modify job varchar(60);`

删除image列
`alter table employee drop image;`

表名改为user
`rename table employee to user;`

修改表的字符集为utf8
`alter table user character set utf8;`

修改列名name为username
`alter table user change name username varchar(100);`

# DML：数据操作语言
作用：向数据库中插入、删除、修改数据
常用关键字：`insert` ,`update`,`delete`
注意：
- mysql中，字符串或者日期要包含在单引号中
- 空值的表示为：null

使用insert语句向表中插入三个员工的信息

`insert into user values (1,'tom','female','1992-3-9','CTO','1000','developer');`

`insert into user (id,username,gender,birthday,job,salary,resume)  values (2,'jack','male','1993-3-9','CTO','2000','developer');`

`insert into user (id,username,gender,birthday,job,salary,resume)  values (3,'Lili','female','1993-3-9','CTO','2000','developer');`

```
mysql> show variables like 'character%';
+--------------------------+--------------------------------+
| Variable_name            | Value                          |
+--------------------------+--------------------------------+
| character_set_client     | gbk     客户端使用的编码
| character_set_connection | gbk    数据库连接时使用的编码
| character_set_database   | utf8     数据库使用的编码
| character_set_filesystem | binary    
| character_set_results    | gbk      查询结果集使用的编码
| character_set_server     | latin1    服务器使用的编码
| character_set_system     | utf8     系统使用的编码
| character_sets_dir       | E:\xampp\mysql\share\charsets\ |
+--------------------------+--------------------------------+
```
告知服务器客户端使用的编码：
`set character_set_client=gbk;`

告知服务器返回的结果集使用gbk：
`set character_set_results=gbk`

查看表中的所有记录
`select * from user;`

将所有员工的薪水修改为3000：
`update user set salary=3000;`

将姓名为“tom”的员工薪水改为2500：
`update user set salary=2500 where username='tom';`

将姓名为"jack" 的员工薪水改为3200，job改为front-end：
`update user set salary=4000,job='font-end' where username='jack';`

将Lili的薪水在原有的基础上增加1000：
`update user set salary=salary+1000 where username='Lili';`

删除表中用户名为Lili的记录：
`delete from user where username='Lili';`

删除表中所有记录：
`delete from user;`

使用truncate删除表中记录(摧毁整张表格，重新建立表结构)
`truncate table user;`  

# DQL 数据查询语言
Date Query Language
作用：查询数据，返回结果集
常用关键字：select

查询所有学生的信息
`select * from student;`

查询表中所有学生的姓名和对应的英语成绩
`select name,english from student;`

过滤表中重复的数据
`select distinct english from student;`

给所有学生数学分数加上10分特长分
`select name,math+10 from student;`

统计每个学生的总分
`select name,chinese+english+math from student;`

使用别名表示学生分数
`select name as 姓名,chinese+english+math 总分 from student;`

查询id=1的学生信息
`select * from student where id=1;`

查询英语分数在80-90之间的学生信息
`select * from student where english between 80 and 90;`

查询数学成绩为89，90,91的学生信息
`select * from student where math in (89,90,91);`

查询姓李的学生信息
`select * from student where name like '李%';`

查询数学成绩大于80，语文成绩大于80的学生
`select * from student where math>80 and chinese>80;`

对数学成绩排序输出
`select name,math from student order by math;`

对总分排序从高到低倒序输出
`select name as 姓名,chinese+english+math 总分 from student order by 总分 desc;`

# 数据完整性
数据完整性是为了保证插入到数据中的数据是正确的，它放防止了用户可能的输入错误。
- 实体（行）完整性
规定表的一行（即每一条记录）在表中是唯一的实体。
通过定义主键约束来实现
主键：primary key （不能为null,且唯一）
	- 逻辑主键：比如ID，不代表实际的业务意义，只是用来标识唯一的一条记录（推荐使用）
	- 业务主键：比如username作为主键
实现方式1：
```
create table t1(
	id int primary key,
	name varchar(100)
	);
```
实现方式2：可以定义联合主键
```
create table t2(
	id int,
	name varchar(100),
	primary key (id)
);
```
实现方式3：（推荐）
```
create table t3(
	id int,
	name varchar(100)
);
alter table t3 add primary key (id);
```
主键自增（Oracle没有）
```
create table t4(
	id int primary key auto_increment,
	name varchar(100)
);
```

- 域（列）完整性
指数据库表的列（即字段）必须符合某种特定的数据类型或约束
数据类型
长度
非空约束（not null）
唯一约束（unique）
```
create table t5(
	username varchar(100) not null unique,
	gender varchar(100),
	phonenumber varchar(100)
);
```

- 参照完整性（多表）外键约束
多表设计：一对多，多对多，一对一
一对多：
```
create table customers(
	id int,
	name varchar(100),
	address varchar(255)
);
create table orders(
	id int primary key,
	order_num varchar(100),
	price float(8,2),
	status int,
	customer_id int,
	constraint customer_id_fk foreign key(customer_id) references customers(id)
);
```

# 多表查询
链接查询
- 交叉链接 （隐式查询，不使用关键字）：
`select * from customers,orders;`  
- 内链接：
`select * from customers c,orders o where c.id=o.customer_id;`
- 外链接：
左外：返回符合链接条件的记录，同时返回左表中不满足链接条件的剩余记录
右外：

几个简单的查询
- 嵌套查询  子查询的语句放到小括号之内。
- 联合查询
- 报表查询

# 分组统计
统计一个班共有多少学生？
`select count(*) from student;`

统计数学成绩大于90分的学生共有多少个
`select count(*) from student where math>90;`

统计一个班的数学总成绩
`select sum(math) from student ;`

注意：可以使用反引号把关键字引起来，当做普通字符串对待
