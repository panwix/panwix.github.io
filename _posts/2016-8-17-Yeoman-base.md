---
layout: post
title: Yeoman 基础
categories: nodeJs
tags: [开源]
fullview: false
---
# Yeoman学习笔记

### 什么是Yeoman
Yeoman是现代web app的脚手架工具

### Yeoman的组成

#### yeoman主要包含了三个工具：yo, grunt, bower:
1. yo: 脚手架工具，主要作用是创建项目骨架。
2. grunt: 构建工具，主要用来运行各种任务，比如文件压缩，合并，打包等。
3. bower: 主要用来做前端资源依赖管理， 跟npm很像，npm管理的是node模块的依赖，bower管理的是前端资源的依赖，如css，javascript文件等

### 什么是Bower
Bower是一个客户端技术的软件包管理器

### 使用Bower的原因
1. 节省时间
2. 脱机工作 在用户主目录下创建一个.bower的文件夹，里面有所有下载过的资源
3. 可以很容易的展现客户端的依赖关系
4. 让升级变的简单

### 使用Bower
	安装：bower install jquery
	列出所有包：bower list
	包的搜索：bower search bootstrap
	包的信息： bower info bootstrap
	包的卸载：bower uninstall jquery
	创建bower.json：bower init

### 什么是Grunt
Grunt是javascript世界的自动化构建工具
