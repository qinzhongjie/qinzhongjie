---
title: gulp自动化构建项目（二）——自动化
date: 2016-09-08 22:08:19
tags:
	gulp
---

我们继续在跟目录下创建`src --> html`，`dist --> html`文件夹，,在`src --> html`下面创建`index.html`文件，现在的结构应该是这样的：
```
myweb
	|----- dist
		  |-----html
	|----- node_modules
	|-----src
		  |-----html
			    |-----index.html
```
<!--more-->

现在在index.html文件中写入`<h1>hello world</h1>`。

### 实现自动拷贝

接下来编写`gulpfile.js`文件，这是实现自动化的关键,目的是把`src --> html`下面的`index.html`文件拷贝到`dist --> html`。

```
//引入gulp模块
var gulp = require('gulp');
//创建任务，任务名为copy
gulp.task('copy',function(){
	//读取文件
	gulp.src('src/html/index.html')
	//写入文件
	.pipe(gulp.dest('dist/html'));
});
```
编写完成后，在控制台用`gulp copy`执行copy任务

![执行命令](http://ob9qd20l4.bkt.clouddn.com/13.jpg)

然后查看`dist --> html`下面已经存在`index.html`文件。

### 创建http服务

下一个任务是创建一个http服务，通过http服务访问`dist --> html`下面的idnex.html。这就需要引入[`browsersync`](https://www.browsersync.io/)插件。先用npm安装，
```
npm install browser-sync --save-dev
```
安装完成后在`gulpfile.js`中增加以下代码块：

```
//引入browser-sync模块并创建一个bs对象
var bs = require('browser-sync').create();
//创建server服务,名为start
gulp.task('start',function(){
	bs.init({
		server:'./dist/html/'
	});
});
```
完成后在控制台调用此任务

![调用http服务](http://ob9qd20l4.bkt.clouddn.com/14.jpg)

打开浏览器访问`localhost:3000`（也可能浏览器会自动打开），出现`Hello World`，按`ctrl+c`关闭服务，任务完成。

### 多窗口同步
接下来是一个有趣的事，如果上面编写的index.html足够长，在同时打开多个浏览器窗口浏览的情况下，所有窗口竟然会同步滚动！如果此时有手机和这台电脑处于同一个局域网络的话，手机访问控制台中`External`提供的URL打开的窗口会和PC上的保持同步！如下图所示效果

![多窗口同步展示](http://ob9qd20l4.bkt.clouddn.com/15.gif)

### 实现监听
现在的任务是实现**只要src中的源文件index.html有所改动，程序会自动拷贝到dist-->html下面（即执行上面编写的copy任务），并且浏览器自动刷新，实现实时浏览**”这里用到了监听事件，继续编写`start`任务：

```
//引入browser-sync模块并创建一个bs对象
var bs = require('browser-sync').create();
//创建server服务,名为start
gulp.task('start',function(){
	bs.init({
		server:'./dist/html/'
	});
	gulp.watch('src/html/index.html',['copy']);
	gulp.watch(['src/html/index.html']).on('change',bs.reload);
});
```
编写完成后在控制台执行start任务，开启http服务。打开多个窗口，发现能实现同步滚动，现在不要关闭浏览器窗口，打开src-->html-->index.html，修改页面内容，发现多个浏览器窗口实时刷新，展示修改后的结果。

![修改实时同步预览](http://ob9qd20l4.bkt.clouddn.com/16.gif)

到此，初步的自动化已经实现了，此处实时刷新的效率与电脑配置有关。

