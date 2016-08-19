---
layout: post
title: jquery 基础
categories: javascript
tags: [开源]
fullview: true
---
## 基础选择器
1. id选择器 $("my_id")
2. element选择器 $("element")
3. class选择器 $(".class")
4. 全选择器 $("*")
5. 多选择器 $("xxx, xxx, xxx")
6. 层次选择器 $("ance desc")
7. 子选择器 $("parent > child")
8. 一个相邻选择器 $("prev + next")
9. 所有相邻选择器 $("prev ~ siblings")

## 过滤性选择器
1. :first过滤选择器 $("li:first")
2. :eq(index)过滤选择器 $("li:eq(3)")
3. :contains(text)过滤选择器 $(li:contains("土豪"))
4. :has(selector)过滤选择器 $("li:has('p')")
5. :hidden过滤选择器 $("p:hidden")
6. :visible过滤选择器
7. [attribute=value]属性选择器 $("li[title='我最爱']")
8. [attribute!=value]属性选择器 $("li[title!='我最爱']")
9. [attribute*=value]属性选择器 $("li[title*='最']")
10. :first-child子元素过滤选择器 $("li:first-children")
11. :last-child子元素过滤选择器

## 表单选择器
1. :input表单选择器 $("#frmTest : input")
2. :text表单文本选择器 $("#frmTest : text")
3. :password表单密码选择器 $("#frmTest: password")
4. :radio单选按钮选择器 $("#frmTest: radio")
5. :checkbox复选框选择器 $("#frmTest: checkbox")
6. :submit提交按钮选择器 $("#frmTest input:submit")
7. :image图像域选择器 $("#frmTest :image")
8. :button表单按钮选择器 $("frmTest: button")
9. :checked选中状态选择器 $("frmTest: checked")
10. :selected选中状态选择器 $("frmTest: selected")

## jQuery操作DOM元素
1. 使用attr()方法控制元素的属性 attr()
2. 操作元素的内容 html() 	text()
3. 操作元素的样式 addClass() css()
4. 移除属性和央样式 removeAttr(name) removeClass(class)
5. 使用append()方法向元素内追加内容
6. 使用appendTo()方法向被选元素内插入内容
7. 使用before()和after()在元素前后插入内容
8. 使用clone()方法复制元素
9. 替换内容 replaceWith() replaceAll()
10. 使用wrap()和wrapInner()方法包裹元素和内容 wrap()包裹元素本身 wrapInner()包裹元素中的内容
11.使用each()方法遍历元素
12.使用remove()和empty()方法删除元素 remove()是删除本身和子元素 empty()只删除子元素

## jQuery事件与应用
1. 页面加载是触发ready()事件 ready()类似与onLoad(),但前者加载完DOM结构，后者要全部元素加载。$(document).ready(function(){})等价于$(function(){})
2. 使用bind()方法绑定元素事件 $(selector).bind(event, [data],function)
3. 使用hover()方法切换事件 $(selector).hover(over, out);
4. 使用toggle()方法绑定多个函数 $(selector).toggle(fun1(),fun2(),funN(),...)
5. 使用unbind()方法移除元素绑定的事件 $(selector).unbind(event,fun)
6. 使用one()方法绑定元素的一次性事件 $(selector).one(event,[data],fun)
7. 调用trigger()方法手动触发指定事件 $(selector).trigger(event)
8. 文本框的focus和blur事件
9. 下拉列表框的change事件 $("select").bind("change", function(){})
10. 使用live()方法绑定元素的事件 $(selector).live(event,[data],fun)可以绑定通过代码提交的元素

## jQuery动画特效
1. 调用show()和hide()方法显示和隐藏元素 $(selector).hide(speed, [callback]),$(selector).show(speed, [callback])
2. 调用toggle()方法实现动画切换效果 $(selector).toggle(speed, [callback])
3. 使用slideUp()和slidDown()方法的滑动效果 $(selector).slideUp(speed, [callback])
4. 使用slideToggle()方法实现图片“变脸”效果 $(selector).slideToggle(speed, [callback])
5. 使用fadeIn()与fadeOut()方法实现淡入淡出效果 $(selector).fadeIn(speed, [callback])
6. 使用fadeTo()方法设置淡入淡出效果的不透明度 $(selector).fadeTo(speed, opacity, [callback])
7. 调用animate()方法制作简单的动画效果 $(selector).animate({params}, speed, [callback])
8. 调用stop()方法停止当前所有动画效果 $(selector).stop([clearQueue],[goToEnd])
9. 调用delay()方法延时执行动画效果 $(selector).delay(duration)

## jQuery实现Ajax应用
1. 使用load()方法异步请求数据 load(url, [data], [callback])
2. 使用getJSON()方法异步加载JSON格式数据 jQuery.getJSON(url,[data],[callback])或$.getJSON(url, [data], [callback])
3. 使用getScript()方法异步执行加载并执行js文件 jQuery.getScript(url, [callback])或$.getScript(url, [callback])
4. 使用get()方法以GET方式从服务器获取数据 $.get(url, [callback])
5. 使用post()方法以POST方式从服务器发送数据 $.post(url, [data], [callback])
6. 使用serialize()方法序列化表单元素值 $(selector).serialize()
7. 使用ajax()方法加载服务器数据 jQuery.ajax([settings])或$.ajax([settings])
8. 使用ajaxSetup()方法设置全局Ajax默认选项 jQuery.ajaxSetup([options])或$.ajaxSetup([options])
9. 使用ajaxStart()和ajaxStop()方法 请求前触发的方法和请求完成后出发的方法

## jQuery常用插件
1. 表单验证插件－－validate
2. 表单插件－－form
3. 图片灯箱插件－－lightBox
4. 图片的放大镜插件－－jqzoom $(linkimage).jqzoom({options})
5. cookie插件－－cookie 保存：$.cookie(key, value);读取：$.cookie(key);删除：$.cookie(key,null)
6. 搜索插件－－autocomplete $(textbox).autocomplete(urlData, [options]);
7. 右键菜单插件－－contextmenu
8. 自定义对象级插件－－lifocuscolor插件 $(Id).focusColor(color)
9. 自定义类级别插件－－twoaddresult $.addNum(p1,p2)和$.subNum(p1,p2)

## jQuery UI型插件
1. 拖拽插件－－draggable $(selector).draggable({options})
2. 放置插件－－droppable $(selector).droppable({options})
3. 拖拽排序插件－－sortable $(selector).sortable({options})
4. 面板折叠插件－－accordion $(selector).accordion({options})
5. 选项卡插件－－tabs $(selector).tabs({options})
6. 对话框插件－－dialog $(selector).dialog({options})
7. 菜单工具插件－－menu $(selector).menu({options})
8. 微调按钮插件－－spinner $(selector).spinner({options})
9. 工具提示插件－－tooltip $(selector).tooltip({options})

## jQuery 工具类函数
1. 获取浏览器的名称与版本信息
	1. 浏览器名称和版本信息 $.browser
	2. 判断特定浏览器 $.browser.chrome, $.browser.mozilla
	3. 浏览器版本信息 $.browser.version
2. 检测浏览器是否属于w3c盒子模型 $.support.boxModel(w3c盒子模型width，height不包含padding和border值)
3. 检测对象是否为空 $.isEmptyObject(object)
4. 检测对象是否为原始对象(对象是否为通过{}或new Object()) $.isPlainObject(obj)
5. 检测两个节点的包涵关系 $.contains(container, contained)
6. 字符串操作函数 $.trim(str)
7. URL操作函数 $.param(object)
8. 使用$.extend()扩展工具函数	$.extend({options})
9. 使用$.extend()扩展Object对象 $.extend(obj1,obj2,...objn)	  
