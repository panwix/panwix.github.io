---
layout: post
title: jekyll学习文档
categories: jekyll
tags: [开源]
fullview: true
---

# jekyll教程

### 简介

jekyll是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档， 通过一个转换器（如Markdown）和我们的Liquid渲染器转化成一个完整的可发布的静态网站。

### 安装

	~ $ gem install jekyll
	~ $ jekyll new myblog
	~ $ cd myblog
	~/myblog $ jekyll server

###基本用法

* jekyll build: 当前文件夹中的内容将会生成到 ./_site 文件夹中
* jekyll build --destination <destination> 当前文件夹中的内容生成到目标文件夹<destination>中
* jekyll build --source <source> --destination <destination> 指定源文件夹<source>中的内容将会生成到目标文件夹<destination>中
* jekyll build --watch 当前文件夹中的内容将会生成到 ./_site 文件夹中, 查看改变,并且自动再生成

###目录结构

	-- _config.yml 保存配置数据
	-- _drafts 草稿
	  |-- begin-width-the-crazy-ideas.textile  
	  |-- on-simplicity-in-technology.markdown
	-- _includes 页面重用部分
	  |-- footer.html
	  |-- header.html
	-- _layouts 包裹在文章外部的模版
	  |--default.html
	  |--post.html
	-- _posts 自己的文章
	  |--2016-05-05-xxx.textile
	-- _site
	-- .jekyll-metadata
	-- index.html    	    
