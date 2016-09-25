---
title: gulp自动化构建项目（一）——环境搭建
date: 2016-09-07 23:15:09
tags:
	gulp
---

gulp是前端开发项目构建构建工具，在开发过程中使用gulp可以避免重复的机械劳动，大大提高开发效率，比如：文件合并，文件拷贝，less编译，css压缩， js压缩，图片压缩等。

gulp官方网站：[gulpjs.com](http://gulpjs.com/)
gulp中文网站：[www.gulpjs.com.cn](http://www.gulpjs.com.cn/)

gulp基于node.js，需要配置node环境。

<!--more-->

### 安装node.js
在[node.js官网](https://nodejs.org/en/)下载最新版node安装包，由于安装包格式为msi，一路确定即可，安装程序会自动配置环境变量。
安装完成在控制台输入指令`node -v`检测是否安装成功，若出现版本号表示安装已安装成功。

### npm
npm是node.js的包依赖管理工具，类似于java中的maven，前端页面依赖包一般也用[bower](https://bower.io/)。
开发者为node.js开发了大量工具包，在[npm官网](https://www.npmjs.com/)可查看具体包信息，按照说明下载使用。由于官网访问速度慢，用[淘宝npm镜像](https://npm.taobao.org/)也可，与官网每十分钟同步一次，基本保持一致。

安装node过程中已经自动安装了npm，默认位置为：`C:\Program Files\nodejs\node_modules\npm`

配置npm的环境变量，通过命令`npm -v`查看npm是否安装成功

![成功安装node.js](http://ob9qd20l4.bkt.clouddn.com/2.jpg)

### 初始化项目文件
接下来我们在E盘根目录创建`myweb`文件夹，表示项目。进入`myweb`项目文件夹，在控制台输入`npm init`初始化，创建package.json配置文件。一路回车即可，直至项目根目录生成`package.json`文件，表示初始化完成。`package.json`文件为本项目配置文件。

### 安装gulp
在控制台输入`npm install gulp --save-dev`安装项目开发依赖包gulp，`--save`表示写入配置文件即`package.json`文件中，`-dev`表示只在开发阶段依赖。安装完成后项目根目录出现`node_modules`文件夹。
控制台输入`gulp -v`检查是否安装成功。出现版本号表示安装成功。
查看`package.json`文件，多了以下信息：
```
"devDependencies": {
    "gulp": "^3.9.1"
  }
```
此时在项目根目录新建文件`gulpfile.js`，注意文件名为固定，不能随意修改。此时项目根目录的情况是这样的：

![两个文件一个文件夹](http://ob9qd20l4.bkt.clouddn.com/3.jpg)

到此，基础环境已搭建完成。