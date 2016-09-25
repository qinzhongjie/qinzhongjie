---
title: gulp自动化构建项目（三）——less编译及文件压缩
date: 2016-09-09 10:19:26
tags:
	gulp
---

本章主要介绍几个常用的插件，用来完成less自动编译，css文件压缩，js文件压缩，html文件压缩等操作。

### less文件编译插件
[gulp-less](https://www.npmjs.com/package/gulp-less)
```
//less文件编译
var less = require('gulp-less');
gulp.task('less',function(){
	gulp.src('src/less/*.less')
	.pipe(less())
	.pipe(gulp.dest('dist/css'));
});
```
<!--more-->

### css文件压缩
[gulp-minify-css](https://www.npmjs.com/package/gulp-minify-css)
```
//less文件编译
var less = require('gulp-less');
//压缩css文件
var mincss = require('gulp-minify-css');

gulp.task('less',function(){
	gulp.src('src/less/*.less')
	.pipe(less())
	.pipe(mincss())   //压缩css文件
	.pipe(gulp.dest('dist/css'));
});

```

### js文件压缩
[uglify](https://www.npmjs.com/package/uglify)
```
//js文件压缩
var uglify = require('gulp-uglify');
gulp.task('minjs',function(){
	gulp.src('src/js/*.js')
	.pipe(uglify())
	.pipe(gulp.dest('dist/js'));
});
```

### html文件压缩
[gulp-htmlmin](https://www.npmjs.com/package/gulp-htmlmin)
```
gulp.task('minhtml',function(){
	//读取文件
	gulp.src('src/html/index.html')
	//html压缩
	.pipe(htmlmin({
			collapseWhitespace: true,
      			removeComments: true
      		}
		))
	//写入文件
	.pipe(gulp.dest('dist/html'));
});
```