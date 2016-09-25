---
title: 什么是webView
date: 2016-04-05 17:01:11
tags:
	- App
---

## 定义
 在Android手机中内置了一款高性能webkit内核浏览器，在SDK中封装为一个叫做WebView（网络视图）的组件。Android4.4的内核是chrome内核，Android4.4以下是Android webkit内核。
> A View that displays web pages. This class is the basis upon which you can roll your own web browser or simply display some online content within your Activity. It uses the WebKit rendering engine to display web pages and includes methods to navigate forward and backward through a history, zoom in and out, perform text searches and more.

<!--more-->

## 事件
webView加载时有3个事件：
 - loading  　 开始载入页面时触发
 - titleupdate 　 载入过程中title已经解析并赋予新值，则触发titleupdate
 - loaded  　	载入完毕触发loaded

## 作用
利用webView的这种方式在有些时候UI布局就可以转成相应的html代码编写了，在UI和视觉效果上就会节省很多时间，而且可以和js交互，为前端打开了一扇大门，于是乎，前端人员华丽丽的开始了移动应用开发。

## 开发（[Hbuilder](http://dcloud.io)）
 - webView是调用原生界面的H5+对象
 - 单个webView只承载单个页面的DOM，多个webView可以组合，套嵌
 - 页面之间会相互遮挡，所以大小很重要
 - 要想使界面流畅，就要合理组合使用webView




