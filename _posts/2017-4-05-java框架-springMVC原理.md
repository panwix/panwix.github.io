---
layout: post
title: springMVC
categories:  java
tags: 框架
fullview: true
---

# Spring MVC 原理
#### spring mvc的工作流
<img src='http://images2015.cnblogs.com/blog/799093/201607/799093-20160724233025107-1243112232.jpg'/>

1. 用户发送请求至前端控制器DispatcherServlet
2. DispatcherServlet收到请求调用HandlerMapping处理器映射器。
3. 处理器映射器找到具体的处理器，生成处理器对象及处理器拦截器（如果有则生成）一并返回给DispatcherServlet
4. DispatcherServlet调用HandlerAdapter处理器适配器
5. HandlerAdapter经过适配调用具体的处理器(Controller,后端控制器)
6. Controller执行完返回ModelAndView
7. HandlerAdapter将controller执行结果ModelAndView返回给DispatcherServlet
8. DispatcherServlet将ModelAndView传给ViewReslover视图解析器
9. ViewReslover解析后返回具体View
10. DispatcherServlet根据view进行渲染视图（即将模型数据填充至视图中）
11. DispatcherServlet响应用户

#### springMVC与struts2的主要区别
1. springMVC的入口是Servlet即前端控制器， 而struts2入口是一个filter过滤器
2. springMVC是基于方法开发，传递参数是通过方法形参，可以设计为单例或多例（建议单例），struts2是基于类开发，传递参数是通过类的属性，只能设计为多例
3. struts采用值栈存储请求和响应数据，通过OGNL存取数据， springmvc通过参数解析器将request对象内容进行解析成方法形参，将响应数据和页面封装成ModelAndView对象，最后又将模型数据通过request对象传输到页面。jsp视图解析器默认使用jstl。
