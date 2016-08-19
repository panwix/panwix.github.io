---
layout: post
title: node 基础
categories: nodeJs
tags: [开源]
fullview: true
---
# nodejs
    nodejs是一个为实时Web应用开发而诞生的平台，它摒弃了传统平台依靠多线程来实现高并发的设计思路，采用了单线程、异步式I/O、事件驱动式的程序设计模型。与PHP、Python、Ruby on Rails相比，它跳过了Apache、Nginx等HTTP服务器，直接面向前端开发。
    nodejs最大的特点就是采用异步式I/O与事件驱动的架构设计。
    Commonjs规范包括了模块（modules）、包（package）、系统(system)、二进制(binart)、控制台(console)、编码(encodings)、文件系统(filesystems)、套接字(sockets)、单元测试(unit testing)等部分
    nodejs提供了exports和require两个对象，其中exports是模块公开的接口， require用于从外部获取一个模块的接口， 即所获取模块的exports对象
`exports.setName=function(){}`
`exports.Hello = Hello`
`module.exports = Helo`

### 本地模式与全局模式的区别
1. 本地模式 可以通过require使用 但不注册PATH
2. 全局模式 不能通过require使用 注册PATH

### 发布包
1. npm init 交互式生成package.json
2. 创建帐号 npm adduser
3. 检测是否取得了帐号 npm whoami
4. 发布 npm publish
5. 取消发布 npm unpublish

### 调试
1. 启动调试工具 node debug debug.js
2. run,restart,c,n,s,o,sb(), sb('f()'),sb('script.js',20),cb(),bt,list(5),watch(expr),unwatch(expr),watchers,repl,kill,scripts,version
3. 远程调试 node --debug[=port] script.js node --debug-brk[=port] script.js
4. 使用node-inspector调试nodejs
	1. 安装 npm install －g node-inspector
	2. 启动 node --debug-brk=5858 debug.js
	3. 启动 node-inspector
	4. 浏览器中 http://127.0.0.1:8080/debug?port=5858

### Express 框架
`Express除了为http模块提供了更高层的接口外，还实现了路由控制，模版解析支持，动态视图，用户会话，CSRF保护，静态文件服务，错误控制器，访问日志，缓存，插件支持`

### 模版引擎
	设置模版引擎:	app.set('views', __dirname + '/views'); app.set('view engine', 'ejs');
