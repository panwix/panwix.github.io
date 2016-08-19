---
layout: post
title: ecmascript语法规范
categories: ecmascript语法规范
tags: [开源]
fullview: true
---

# ECMAScript语法

###### ECMAScript是一种由Ecma国际（前身为欧洲计算机制造商协会）通过ECMA－262标准化的脚本程序设计语言。现在最新版应该是2015年6月17日发布的ECMAScript 6正式版即ECMAScript 2015(官方名称).

#### 基础
1. 区分大小写
2. 变量是弱类型
3. 结尾的；可有可无
4. 注释和java一样
5. 括号代表代码块
6. 变量声明不是必须的（ECMAScript 的解释程序遇到未声明过的标识符时，用该变量名创建一个全局变量，并将其初始化为指定的值。）
7. 关键字 break case catch continue default delete do else finally for function if in instanceof new return switch this throw try typeof var void while with
8. 保留字 abstract boolean byte char class const debugger double enum export extends final float goto implements import int interface long native package private protected public short static super synchronized throws transient volatile
9. 值：分为原始值和引用值（类型可以通过typeof的到）
	1. 原始值 存储在栈（stack）中的简单数据段  Undefined、Null、Boolean、Number、String（有个小坑 null == undefined，值 undefined 实际上是从值 null 派生来的）
	2. 引用值 存储在堆（heap）中的对象
10. 类型转化 toString()、parseInt()、parseFloat()
11. 强制类型转换	Boolean()、Number()、String()
12. 引用类型 ECMAScript中的所有对象都由Object对象继承而来
13. Object对象属性:
	1. constructor 对创建对象的函数的引用（指针）
	2. prototype 对该对象的对象原型的引用
14. Object对象方法
	1. hasOwnProperty(property) 判断对象是否有某个特定的属性
	2. IsPrototypeOf(object) 判断该对象是否为另一个对象的原型
	3. PropertyIsEnumerable
	4. 判断给定的属性是否可以用 for...in 语句进行枚举。
	5. ToString() 返回对象的原始字符串表示
	6. ValueOf() 返回最适合该对象的原始值 一般与ToString()相同

#### 常用对象和方法
1. Boolean
2. Number
	1. toFixed() toFixed() 方法返回的是具有指定位数小数的数字的字符串表示
	2. toExponential() 用科学计数法表示的数字的字符串形式
	3. toPrecision() 据最有意义的形式来返回数字的预定形式或指数形式
3. String
	1. length属性
	2. charAt()
	3. charCodeAt() 返回字符码
	4. concat()字符串连接 新创建了个对象，原来对象不变
	5. indexOf()
	6. lastIndexOf()
	7. slice() 字符串切割 负数按长度＋负数来
	8. substring() 字符串切割 负数按0来
	9. toLowerCase()、toLocaleLowerCase()、toUpperCase() 和 toLocaleUpperCase()
	10. instanceof 运算符与 typeof 运算符相似，用于识别正在处理的对象的类型

#### ECMAScript特有的运算符与语句
1. delete 删除对象的属性和方法
2. for-in 语句 for (property in expression) statement
3. label : statement 标签语句 标签可以被之后的 break 或 continue 语句引用
4. with (expression) statement 用于设置代码在特定对象中的作用域

#### ECMAScript函数
函数是 ECMAScript 的核心，ECMAScript的函数实际上是功能完整的对象

1. arguments 对象 在函数代码中，使用特殊对象 arguments，开发者无需明确指出参数名，就能访问它们
2. 可以用 Function 类直接创建函数， 最后一个参数是函数主体（要执行的代码）
3. Function 对象的 length 属性 声明了函数期望的参数个数
4. valueOf() 方法和 toString() 方法返回函数的源码
5. 闭包，指的是词法表示包括不被计算的变量的函数，也就是说，函数可以使用函数之外定义的变量

#### ECMAScript对象
1. 类型
	1. 本地对象：Object Function Array String Boolean Number Date RegExp E	EvalError RangeError ReferenceError SyntaxError TypeError URIError

	2. 内置对象：Global、Math

	3. 宿主对象：所有非本地对象都是宿主对象
2. 作用域 公用作用域
	1. 私有作用域解决方法：`obj._color_ = "blue";`
	2. 静态作用域解决方法： 函数是对象，对象可以有属性和方法

#### ECMAScript创建对象
1. 函数封装创建对象的代码，参数传递特有的属性值 有问题
2. 构造函数方法 有问题

		function Car(sColor,iDoors,iMpg) {
  			this.color = sColor;
  			this.doors = iDoors;
  			this.mpg = iMpg;
  			this.showColor = function() {
    			alert(this.color);
  			};
		}
		var oCar1 = new Car("red",4,23);
		var oCar2 = new Car("blue",3,25); 	
3. 原型方式 有问题

		function Car() {
		}

		Car.prototype.color = "blue";
		Car.prototype.doors = 4;
		Car.prototype.mpg = 25;
		Car.prototype.showColor = function() {
  			alert(this.color);
		};

		var oCar1 = new Car();
		var oCar2 = new Car();
4. 混合的构造函数/原型方式

		function Car(sColor,iDoors,iMpg) {
  			this.color = sColor;
  			this.doors = iDoors;
  			this.mpg = iMpg;
  			this.drivers = new Array("Mike","John");
		}

		Car.prototype.showColor = function() {
  			alert(this.color);
		};

		var oCar1 = new Car("red",4,23);
		var oCar2 = new Car("blue",3,25);

		oCar1.drivers.push("Bill");

		alert(oCar1.drivers);	//输出 "Mike,John,Bill"
		alert(oCar2.drivers);	//输出 "Mike,John"

5. 动态原型方法

		function Car(sColor,iDoors,iMpg) {
  			this.color = sColor;
  			this.doors = iDoors;
  			this.mpg = iMpg;
 			this.drivers = new Array("Mike","John");
  			if (typeof Car._initialized == "undefined") {
    			Car.prototype.showColor = function() {
     	 			alert(this.color);
    			};
    			Car._initialized = true;
  			}
		}				
6. 混合工厂方式

		function Car() {
  			var oTempCar = new Object;
  			oTempCar.color = "blue";
  			oTempCar.doors = 4;
  			oTempCar.mpg = 25;
  			oTempCar.showColor = function() {
    			alert(this.color);
  			};
  			return oTempCar;
		}
	目前使用最广泛的是混合的构造函数/原型方式，动态原始方法也很流行，在功能上与构造函数/原型方式等价

#### 修改对象属性方法通过prototype来修改或添加对象的属性和方法

#### ECMAScript对象的继承机制实现
	1. 对象冒充
	function ClassB(sColor, sName) {
    this.newMethod = ClassA;
    this.newMethod(sColor);
    delete this.newMethod;

    this.name = sName;
  	  this.sayName = function () {
     	 alert(this.name);
   	  };
	}
	2. 原型链 弊端是不支持多继承
	function ClassA() {
	}

	ClassA.prototype.color = "blue";
	ClassA.prototype.sayColor = function () {
    	alert(this.color);
	};

	function ClassB() {
	}

	ClassB.prototype = new ClassA();

## ECMASCript 6

### 变量

1. 新增了let和const命令 所在代码块内有效		
2. 变量的解构赋值

### 字符串

1. ES6加强了对Unicode的支持，并且扩展了字符串对象：增加了codePointAt(),String.fromCodePoint(),字符串便利器接口， at(), normalize()， includes(), startWith(), endswith(), repeat(), padStart(), padEnd(),String.raw()

### 数值
1. 二进制 0b
2. 八进制 0o
3. Number.isFinite(), Number.isNaN()
4. Number.parseInt(), Number.parseFloat()
5. Number.isInteger() 25.0也被认为是整数
6. Number.EPSILON 极小常量
7. Number.isSafeInteger()
8. Math.trunc()去除一个数的小数部分，返回整数部分
9. Math.sign() 判断一个数到底是正数、负数、还是零
10. Math.cbrt() 计算一个数的立方根
11. Math.clz32()返回一个数的32位无符号整数形式有多少个前导0
12. Math.imul() 返回两个数以32位带符号整数形式相乘的结果，返回的也是一个32位的带符号整数
13. Math.fround()返回一个数的单精度浮点数形式
14. Math.hypot() 返回所有参数的平方和的平方根
15. 新增对数相关方法：Math.expm1()，Math.log1p(），Math.log10()，Math.log2()
16. 新增三角函数：Math.sinh(x)， Math.cosh(x)，Math.tanh(x)，Math.asinh(x)，Math.acosh(x)，Math.atanh(x)

### 函数
1. 函数参数默认值 指定了默认值以后，函数的length属性，将返回没有指定默认值的参数个数
2. rest参数 ...变量名
3. 扩展运算符 ... 将一个数组转为用逗号分隔的参数序列
	1. 替代数组的apply方法
	2. 合并数组
	3. 函数返回值为数组通过... 相当于返回多个值
	4. 将字符串变数组
	5. 实现了Iterator接口的对象
4. name属性
5. 箭头函数

		var f = v => v;
		相当于
		var f = function(v) {
  			return v;
		};		
	注意点

	1. 函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象
	2. 不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误
	3. 不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替
	4. 不可以使用yield命令，因此箭头函数不能用作Generator函数(可以把yield理解成一种特殊形式的return，它和return一样，会立即把执行权返回父级函数。特别之处在于，yield后面跟的函数或对象会跟一个条件判断，当条件满足时，就会再次回调包含该yield的子函数，并且从yield语句之后继续执行。条件满足之前，执行父函数下面的语句，可以看作异步执行)
	5. 函数绑定运算符是并排的两个双冒号（::）es7里的东西
	6. 尾调用（函数的最后一步是调用另一个函数）尾调用由于是函数的最后一步操作，所以不需要保留外层函数的调用帧，因为调用位置、内部变量等信息都不会再用到了，只要直接用内层函数的调用帧，取代外层函数的调用帧就可以了 递归就不会内存溢出了`尾调用模式仅在严格模式下生效`

### 对象
1. 支持简洁写法

		var birth = '2000/01/01';

		var Person = {
  			name: '张三',
  			//等同于birth: birth
  			birth,
  			// 等同于hello: function ()...
  			hello() { console.log('我的名字是', this.name); }
		};
