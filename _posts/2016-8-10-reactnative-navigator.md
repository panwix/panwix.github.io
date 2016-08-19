---
layout: post
title: navigator用法
categories: react-native
tags: [开源]
fullview: true
---
# React Native Navigator

#### 入口
		<Navigator
			initialRoute={{ name: defaultName, component: defaultComponent }}
			configureScene={(route) => {
				return Navigator.SceneConfigs.VerticalDownSwipeJump;
			}}
			returnScene={(route, navigator) => {
				let Component = route.component;
				return <Component {...route.params} navigator={navigator} />
			}}
		/>

		initialRoute: 指定默认页面
		configureScene: 跳转时的动画 注：node_modules/react-native/Libraries/CustomComponents/Navigator/NavigatorSceneConfigs.js包含所有可用动画
		returnScene: 渲染组件，传递属性（页面跳转需要用到navigator）

#### 跳转页面中
		<TouchableOpacity onPress={this._pressButton.bind(this)>
			<Text>点击事件</Text>
		</TouchableOpacity>

		TouchableOpacity： 用来获取点击事件，相当于拥有特效的onclick()方法

		_pressButton() {
			const { navigator } = this.props;
			if(navigator) {
				navigator.push({
					name: 'nextComponent',
					component: nextComponent,
				})
		}

		navigator是之前传递过来的属性, 通过push方法跳转到下一个组件


#### navigator所有跳转方法
	1. getCurrentRoutes() - h获取当前栈里的路由，也就是push进来，没有pop掉的那些
	2. jumpBack() - 跳回之前的路由并保留现在的
	3. jumpForward() - 跳回到上一个路由
	4. jumpTo(route) － 跳转到已有的场景并且不卸载
	5. push(route) - 跳转到新的场景
	6. pop() - 跳转回去并且卸载掉当前场景
	7. replace(route) - 用一个新的路由替换掉当前场景
	8. resetTo(route) - 跳转到新的场景，并且重置整个路由栈
	9. immediatelyResetRouteStack(routeStack) - 用新的路由数组来重置路由栈
	10. popToRoute(route) - pop到路由指定的场景， 在整个路由栈中， 处于指定场景之后的场景将会被卸载
	11. popToTop() - pop到栈中的第一个场景， 卸载掉所有的其他的场景
#### 参数传递
		if(navigator) {
			navigator.push({
				name: 'nextComponent',
				component: nextComponent,
				params: {
					id: this.state.id
				}
			})
		}

		params来历： return <Component {...route.params} navigator={navigator} />
		这个语法是把routes.params里的每个key作为props的一个属性
