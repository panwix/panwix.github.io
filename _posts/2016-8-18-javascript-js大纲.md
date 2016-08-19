---
layout: post
title: js大纲
categories: javascript
tags: [开源]
fullview: true
---
## 基础
1. 输出内容 document.write()
2. 消息对话框 alert()
3. 消息对话框 confirm()
4. 消息对对话框 prompt(str1, str2)
5. 打开新窗口 window.open([url],[窗口名称],[参数字符串])
6. 关闭窗口 window.close()
7. 通过id获取元素 document.getElementById("id")
8. 替换html元素内容 document.getElementById("id").innerHTML
9. 改变html样式 Object.style.property = new style
10.显示和隐藏 Object.style.display = none|block
11. 控制类名(用来更改样式) object.className = classname
12. 鼠标单击事件:onclick
13. 鼠标经过事件:onmouseover
14. 鼠标移开事件:onmouseout
15. 光标聚焦事件:onfocus
16. 失焦事件:onblur
17. 内容选中事件:onselect
18. 文本框内容改变事件:onchange
19. 加载事件:onload
20. 卸载事件:onunload
21. 字符串大写:toUpperCase()

## js内置对象
1. Date日期对象:
2. String字符串对象
	1. 返回指定位置的字符 charAt(index)
	2. 返回字符串首次首次出现的位置 indexOf(substring, startpos)
	3. 字符串分割 split(",", 3)
	4. 提取字符串 substring()
	5. 提取指定数目的字符 substr()
3. Math对象
	1. 向上取整 ceil()
	2. 向下取整 floor()
	3. 四舍五入 round()
	4. 随机数 random()
4. Array数组对象
	1. 数组连接 concat()
	2. 指定分隔符连接数组元素 join()
	3. 选定元素 slice(start, end)
	4. 颠倒数组元素顺序 reverse()
5. Window对象
	1. 计时器 setTimeout() clearTimeout() setInterval() clearInterval()
	2.History对象 window.history.length|back()|forward()|go()
	3. screen对象 availHeight availWidth colorDepth height height width
6.Location对象location.hash|host|hostname|href|pathname|port|protocol|search|assign()|reload()|replace()
7. Navigator对象 检测浏览器与操作系统的版本 appCodeName appName appVersion platform userAgent
8. Dom对象
	1. 节点属性 nodeName nodeType:(元素：1， 属性：2， 文本：3， 注释：8， 文档：9) nodeValue
	2. 遍历节点树 childNodes firstChild lastChild parentNode nextSibling previousSibling
	3. Dom操作 createElement(element) createTextNode() appendChild() insertBefore() removeChild() replaceChild()
	4. 获取元素 getElementByID(), getElementByName(), getElementByTagName()
	5. 获取属性 elementNode.getAttribute(name)
