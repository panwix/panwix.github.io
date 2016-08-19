---
layout: post
title: freemarker
categories: 前段模版
tags: [开源]
fullview: true
---

# FreeMarker学习：

## FreeMarker解析点：
1. ${...}插值
2. FTL tag标签
3. Comments注释
4. directives指令 if list include

## FreeMarker处理不存在的变量
1. ${user!"Anonymous"}
2. <#if user??></#if>

## FreeMarker中的容器
1. 哈希表
2. 序列
3. 集

## 创建一个库
<#import "/lib/my_test.ftl" as my>
在引入的命名空间上编写变量<#assign mail=xxx@xx.com in my>
