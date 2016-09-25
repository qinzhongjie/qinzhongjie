---
title: 一篇教程掌握HTML
date: 2016-03-18 10:04:32
tags:
	HTML
---
>HTML 指超文本标签语言

<!--more-->

一个基本的HTML页面结构
```
<!DOCTYPE html>
<html>
	<head>
		<title>文档的标题</title>
	</head>

	<body>
	文档的内容......
	</body>

</html>
```
`<!DOCTYPE>`
 - <!DOCTYPE> 声明不是 HTML 标签；它是指示 web 浏览器关于页面使用哪个 HTML 版本进行编写的指令。
 - 所有浏览器都支持 <!DOCTYPE> 声明。
 
`<a> 标签`
 - 链接的默认外观是
	 - 未被访问的链接带有下划线而且是蓝色的
	 - 已被访问的链接带有下划线而且是紫色的
	 - 活动链接带有下划线而且是红色的
 - 大多数图形浏览器都会在作为锚的一部分的图像周围放置特殊的边框。通过在 `<img>` 标签中把图像的 border 属性设置为 0 可以删除超链接的边框
 - 属性
	 - href：
		 - 绝对 URL - 指向另一个站点（比如 href="http://www.example.com/index.htm"）
		 - 相对 URL - 指向站点内的某个文件（href="index.htm"）
		 - 锚 URL - 指向页面中的锚（href="#top"）
	 - target　*标签的 target 属性规定在何处打开链接文档*，属性值有：
		 - _blank  　在新窗口中打开被链接文档
		 - _self　默认。在相同的框架中打开被链接文档
		 - _parent　在父框架集中打开被链接文档
		 - _top　在整个窗口中打开被链接文档
		 - framename　在指定的框架中打开被链接文档 (框架中打开的效果)


`<abbr>`
 - <abbr> 标签指示简称或缩写，比如 "WWW" 或 "NATO"，通过对缩写进行标记，您能够为浏览器、拼写检查和搜索引擎提供有用的信息
 - IE 6 或更早版本的 IE 浏览器不支持 <abbr> 标签
 - 可以在 <abbr> 标签中使用全局的 title 属性，这样就能够在鼠标指针移动到 <abbr> 元素上时显示出简称/缩写的完整版本


`<address>`
 - `<address> `标签定义文档或文章的作者/拥有者的联系信息
 - 所有浏览器都支持 `<address>` 标签
 - `<address>` 标签不应该用于描述通讯地址，除非它是联系信息的一部分
 - `<address>` 元素通常连同其他信息被包含在 <footer> 元素中


`<article>`
 - 功能：定义文章
 - Internet Explorer 8 以及更早的版本不支持 `<article>` 标签
 - <article> 元素的潜在来源：
	 - 论坛帖子
	 - 报纸文章
	 - 博客条目
	 - 用户评论


