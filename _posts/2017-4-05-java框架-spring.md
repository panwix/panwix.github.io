---
layout: post
title: spring
categories:  java
tags: 框架
fullview: true
---

# Spring
#### 什么是spring
Spring是一个开源的Java EE开发框架。

#### spring有哪些优点
* 轻量级:Spring在大小和透明性方面绝对是属于轻量级的，基础版本的Spring框架大约只有2MB
* 控制反转(IOC):Spring使用控制反转技术实现了松耦合。依赖被注入到对象，而不是创建或寻找依赖对象
* 面向切片(AOP):Spring支持面向切面编程，同时把应用的业务逻辑与系统的服务分离开来
* 容器:Sping包含并管理应用程序对象的配置及生命周期
* MVC框架:Spring的web框架是一个设计优良的web mvc框架，很好取代了一些web框架
* 事务管理:Spring对下至本地业务上至全局业务(JAT)提供了统一的事务管理接口
* 异常处理:Spring提供一个方便的API将特定技术的异常(由JDBC, Hibernate, 或JDO抛出)转化为一致的、Unchecked异常。

#### 解释核心容器(应用上下文)模块
这是spring的基本模块，它提供了Spring框架的基本功能。BeanFactory是所有Spring应用的核心。Spring框架是建立在这个模块之上的，这也使得Spring成为一个容器。

#### BeanFactory
BeanFactory是工厂模式的一种实现，它使用控制反转将应用的配置和依赖与实际的应用代码分离开来。

#### Spring 事务
spring只是控制数据库的事务提交和回滚，借助于java的反射机制，在事务控制的方法（通常是service层的方法）前后获取事务开启session，然后执行你的数据操作，如果你的方法内有异常被抛出，spring会捕获异常并回滚你在这个方法内所有的数据操作，如果成功则提交所有的数据，最后spring会帮你关闭需要关闭的东西。所以spring想要做的是，要程序员专注于写逻辑，不需要关系数据库何时开启和关闭连接。

#### Ioc优点
IOC或依赖注入减少了应用程序的代码量。它使得应用程序的测试很简单，因为在单元测试中不再需要单例或JNDI查找机制。简单的实现以及较少的干扰机制使得松耦合得以实现。IOC容器支持勤性单例及延迟加载服务。

#### spring中的依赖注入
依赖注入作为控制反转（IOC）的一个层面，可以有多种解释方式。在这个概念中，你不用创建对象而只需要描述如何创建它们。你不必通过代码直接的将组件和服务连接在一起，而是通过配置文件说明哪些组件需要什么服务。之后Ioc容器负责衔接。

#### 有哪些不同类型的IOC（依赖注入）？
* 构造器依赖注入
* Setter方法依赖注入

#### 如何定义bean的作用域
在Spring中创建一个bean的时候，我们可以声明它的作用域。只需要在bean定义的时候通过’scope’属性定义即可。例如，当Spring需要产生每次一个新的bean实例时，应该声明bean的scope属性为prototype。如果每次你希望Spring返回一个实例，应该声明bean的scope属性为singleton。

#### Spring中支持的5种bean作用域
* singleton: 在Spring IOC容器中仅存在一个Bean实例，Bean以单实例的方式存在
* prototype: 一个bean可以定义多个实例
* request: 每次HTTP请求都会创建一个新的Bean。该作用域仅适用于WebApplicationContext环境
* session: 一个HTTP Session定义一个Bean。该作用域仅适用于WebApplicationContext环境.
* globalSession：同一个全局HTTP Session定义一个Bean。该作用域同样仅适用于WebApplicationContext环境.

bean默认的scope属性是’singleton‘。

#### 解释aop
面向切片编程，或aop允许程序员模块化横向业务逻辑，或定义核心部分功能，例如日志管理和事务管理。

#### 切片（Aspect）
AOP的核心就是切面，它将多个类的通用行为封装为可重用的模块。该模块含有一组api提供cross－cutting功能。例如，日志模块称为日志的aop切面。根据需求的不同，一个应用程序可以有若干切面。在spring aop中，切面通过带有@Aspect注解的类实现。

#### 连接点(jion point)
连接点代表应用程序中插入AOP切面的地点。它实际上是Spring AOP框架在应用程序中执行动作的地点。

#### 通知(advice)
通知表示在方法执行前后需要执行的动作。实际上它是Spring AOP框架在程序执行过程中触发的一些代码。

* Spring切面可以执行一下五种类型的通知:

* before(前置通知)：在一个方法之前执行的通知。

* after(最终通知)：当某连接点退出的时候执行的通知（不论是正常返回还是异常退出）。

* after-returning(后置通知)：在某连接点正常完成后执行的通知。

* after-throwing(异常通知)：在方法抛出异常退出时执行的通知。

* around(环绕通知)：在方法调用前后触发的通知。

#### 切入点
切入点是一个或一组连接点，通知将在这些位置执行。可以通过表达式或匹配的方式指明切入点
