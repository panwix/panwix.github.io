---
layout:     post
title:      react-native 学习文档
subtitle:   " \"Hello World, Hello Blog\""
date:       2016-08-10
author:     "Panwix"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 前端开发
    - react-native
---

### 组件的生命周期

##### 实例化
* getDefaultProps
* getInitalState
* componentWillMount
* render
* compentDidMount

##### 存在期
* componentWillReceiveProps
* shouldCompentUpdate
* compoentWillUpdate
* render
* compentDidUpdate

##### 销毁&清理期
* componentWillUnmount

##### render(创建虚拟dom)
* 只能通过this.props和this.state访问数据
* 可以返回null、false或者任何React组件
* 只能返回一个顶级组件（不能返回一组元素）
* 必须纯净，不能改变组件的状态或者修改DOM的输出

##### componentDidMount
* 通过this.getDomNode()操作渲染出来的元素

### 样式声明
	var styles = StyleSheet.create({
  		base: {
    		width: 38,
    		height: 38,
  		},
  		background: {
    		backgroundColor: '#222222',
  		},
  		active: {
    		borderWidth: 2,
    		borderColor: '#00ff00',
  		},
	});

### 图片
	1. 网络图片
	<Image source={{uri: 'https://facebook.github.io/react/img/logo_og.png'}}
       style={{width: 400, height: 400}} />
    2. 本地图片
    <Image source={require('./my-icon.png')} />

### 触摸事件
* `View.props.onStartShouldSetResponder: (evt) => true`  在用户开始触摸的时候（手指刚刚接触屏幕的瞬间），是否愿意成为响应者
* `View.props.onMoveShouldSetResponder: (evt) => true` 如果View不是响应者，那么在每一个触摸点开始移动（没有停下也没有离开屏幕）时再询问一次：是否愿意响应触摸交互
* 以上两个方法中有返回为true
* `View.props.onResponderGrant: (evt) => {}` View现在要开始响应触摸事件了。这也是需要做高亮的时候，使用户知道他到底点到了哪里
* `View.props.onResponderReject: (evt) => {}` 响应者现在“另有其人”而且暂时不会“放权”，请另作安排
* view开始响应触摸事件:
	1. `View.props.onResponderMove: (evt) => {}`用户正在屏幕上移动手指时（没有停下也没有离开屏幕）
	2. `View.props.onResponderRelease: (evt) => {}` 触摸操作结束时触发，如"touchUp"（手指抬起离开屏幕）
	3. `View.props.onResponderTerminationRequest: (evt) => true` 有其他组件请求接替响应者，当前的View是否“放权”？返回true的话则释放响应者权力。
	4. `View.props.onResponderTerminate: (evt) => {}`响应者权力已经交出
* evt是合成事件(nativeEvent)
	* changedTouches
	* identifier
	* locationX
	* locationY
	* pageX
	* pageY
	* target
	* timestamp
	* touches
