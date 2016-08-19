---
layout: post
title: Express 基础
categories: nodeJs
tags: [开源]
fullview: true
---
# Express笔记

### 路由
	var express = require('express')
	var app express();

	app.get('/', function(req, res){
		res.send('hello world');
	});

### 路由方法
	get, post, put, delete

### 路径路由
	app.get('/ab?cd', function(req, res){
		res.send('ab?cd');
	});

### 路由句柄
	app.get('/example/b', function(req, res, next){
		console.log('response will be sent by the next function ... ');
		next();
	}, function(req, res) {
		res.send('Hello from B!');
	});

### 响应方法
1. res.download()
2. res.end()
3. res.json()
4. res.jsonp()
5. res.redirect()
6. res.render()
7. res.send()
8. res.sendFile()
9. res.sendStatus()

### 使用app.route()创建路由路径的链式路由句柄
	app.route('/book')
		.get(function（req, res）{
			res.send('Get a random book');
		})
		.post(function(req, res) {
			res.send('Add a book');
		})
		.put(function (req, res) {
			res.send('Update the book');
		})

### 使用express.Router()创建模块化, 可挂载的路由句柄
	-- birds.js
	var express = require('express');
	var router = express.Router();

	//该路由使用的中间件
	router.use(function timeLog(req, res, next) {
		console.log('Time:' Date.now());
		next();
	});

	//定义网站主页的路由
	router.get('/', function(req, res) {
		res.send('Birds home page');
	})

	//定义about页面的路由
	router.get('/about', function(req, res){
		res.send('About birds');
	});

	module.exports = router;

	var birds = require('./birds');
	...
	app.use('/birds', birds);		
