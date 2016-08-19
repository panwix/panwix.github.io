---
layout: post
title: react-native 验证器
categories: react-native
tags: [开源]
fullview: true
---

# React 验证器

#### js基本数据类型

* React.PropTypes.array
* React.PropTypes.bool
* React.PropTypes.func
* React.PropTypes.number
* React.PropTypes.object,
* React.PropTypes.string

#### 可以被渲染的对象 number, strings, elementes或array
* React.PropTypes.node

#### React元素
* React.PropTypes.element

#### 用js的instanceOf 操作符声明prop为类的实例
* React.PropTypes.instanceOf(Message)

#### 用enum来限制prop只接受指定的值
* React.PropTypes.oneOf(['News','Photos'])

#### 可以是多个对象类型中的一个
* React.PropTypes.oneOfType([React.PropTypes.string,React.PropTypes.number])

#### 指定类型组成的数组
* React.PropTypes.arrayOf(React.PropTypes.number)

#### 指定类型的属性构成的对象
React.PropTypes.objectOf(React.PropTypes.number)

#### 特定shape参数的对象
React.PropTypes.shape({color: React.PropTypes.string, fontSize: React.PropTypes.number})

#### 任意类型加上isRequired来使prop不可为空
React.PropTypes.func.isRequired

#### 不可空的任意类型
React.PropTypes.any.isRequired
