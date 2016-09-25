---
title: lab
date: 2016-09-18 23:08:32
---

## Angular实现“我的豆瓣”项目

## [<font color=#28993B>[点击此处打开项目]</font>](http://uranux.com:9090/)

------

”我的豆瓣“项目是学习AngularJS过程中开发的一个关于电影数据的展示，数据来自于豆瓣api，使用到了路由，数据绑定等经典知识点。
数据来源于[豆瓣api](https://developers.douban.com/wiki/?title=guide)

## 精彩回顾

### 1、$route 路由
依赖于`ngRoute`模块，此模块独立成单独文件单独发行。
单页面应用通过路由来分发请求，将不同的请求分发给不同的控制器，不同的控制器使用不同的页面来展示数据，在项目中通过路由分配请求路径：
```
module.config(['$routeProvider', function($routeProvider) {
  	$routeProvider.when('/:category/:page', {
    	templateUrl: 'movie_list/view.html',
    	controller: 'MovieListController'
  	});
}])
```
一个路由的简单用法：
项目目录：
```
routedemo
	-------index.html
	-------js
			|--------ngroute.js
	-------view
			|-------view.html
```

index.html：
```
	<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>路由的简单使用</title>
	</head>
	<body ng-app="app">
		<a href="#/view1">[view1]</a><a href="#/view2">[view2]</a>
		<!-- 视图 -->
		<div id="div" ng-view></div>
		<script type="text/javascript" src="node_modules/angular/angular.js"></script>
		<!-- 路由依赖 -->
		<script type="text/javascript" src="node_modules/angular-route/angular-route.js"></script>
		<script type="text/javascript" src="js/ngroute.js"></script>
	</body>
</html>
```

ngroute.js:
```
(function(angular){
	'use strict';
	//依赖于ngRoute模块
	var app = angular.module('app', ['ngRoute']);
	app.config(['$routeProvider',function($routeProvider) {
		$routeProvider
		.when('/view1', {
			controller: 'AppController1',
			templateUrl: './view/view.html'
		})
		.when('/view2', {
			controller: 'AppController2',
			templateUrl: './view/view.html'
		})
		.otherwise({
			redirectTo:'/view1',
		});
	}]);
	app.controller('AppController1', ['$scope', function($scope){
		$scope.message = '控制器1';
	}]);
	app.controller('AppController2', ['$scope', function($scope){
		$scope.message = '控制器2';
	}]);
})(angular)
```

view.html:
```
<p>{{message}}</p>
```

![完成效果](http://ob9qd20l4.bkt.clouddn.com/route1.gif)

.when中的路径是从url的第一个#后的路径开始算起的。
