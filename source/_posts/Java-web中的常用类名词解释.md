---
title: Java web中的常用类名词解释
date: 2016-07-10 10:47:23
tags:
	Java web
---

DBCP（DataBase Connection Pool）
数据库连接池。是 apache 上的一个 java 连接池项目，也是 tomcat 使用的连接池组件。单独使用dbcp需要2个包：commons-dbcp.jar,commons-pool.jar由于建立数据库连接是一个非常耗时耗资源的行为，所以通过连接池预先同数据库建立一些连接，放在内存中，应用程序需要建立数据库连接时直接到连接池中申请一个就行，用完后再放回去。

Dbutils
是Apache组织提供的一个对JDBC进行简单封装的开源工具类库，使用它能够简化JDBC应用程序的开发，同时也不会影响程序的性能。传统操作数据库的类指的是JDBC（java database connectivity：java数据库连接，java的数据库操作的基础API。）。

JSTL
JSTL（JSP Standard Tag Library，JSP标准标签库)是一个不断完善的开放源代码的JSP标签库，是由apache的jakarta小组来维护的。JSTL只能运行在支持JSP1.2和Servlet2.3规范的容器上，如tomcat 4.x。在JSP 2.0中也是作为标准支持的。

<!--more-->

