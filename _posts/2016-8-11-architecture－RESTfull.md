---
layout: post
title: RESTful架构理解
categories: 架构
tags: [开源]
fullview: false
---


# RESTful 架构理解

## REST 即Representational State Transfer, 即表现层状态转化

### 资源(Resource)
表现层指的是“资源”的“表现层”，URI是每个资源的地址是独一无二的识别符。它就代表资源。

### 表现层(Representation)
HTTP请求的头信息中用Accept和Content-Type字段指定，这两个字段才是对“表现层”的描述。

### 状态转化(State Transfer)
四个操作方式的动词：GET用来获取资源，POST用来新建资源(也可以用来更新资源)，PUT用来更新资源，DELETE用来删除资源

### 综述
什么是RESTful架构:

1. 每个URI代表一种资源
2. 客户端和服务器之间，传递这种资源的某种表现层
3. 客户端通过四个HTTP动词，对服务器端资源进行操作，实现“表现层状态转化”
