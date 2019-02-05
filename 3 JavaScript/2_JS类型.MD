## 2_JS类型
- 基本数据类型
	- Undefined
	- Null
	- Boolean
	- String
	- Number
	- Symbol（ES6)
- 引用数据类型
	- Object

### 1 Undefined
- **定义**：表示**未定义**，任何变量赋值前是`Undefined`类型，值为`undefined`
- **特点**：
	- 使用 `typeof` 检查时，会返回`undefined`
	- 类型只有一个值就是`undefined`
	- `undedined`实际是一个变量，而非关键字，为以防其无意被篡改，使用`void 0`来获取`undefined`值（ES5之后设置不允许篡改）
	- 任何数字和`undefined`运算都是`NaN`

### 2 Null
- **定义**：表示**定义了**但是为空，专门用来表示一个为空的对象
- **特点**：
	- 使用 `typeof `检查时，会返回`object`
	- 类型只有一个值就是`null`
	- `null`是关键字，可以放心使用，可以使用`===`来判断
	- 任何数字和`null`运算，`null`可看做`0`运算
- **比较**：
	- `null == undefined`结果为`true`
	- `null === undefined`结果为`false`   

### 3 Boolean
- **定义**：表示逻辑意义上的**真**和**假**
- **特点**：
	- 类型只有`true`和`false`两个值
	- `null`、`undefined`、`0`、`NaN`和空字符串`''`视为false，其他值一概视为true

### 4 String
- **定义**：表示**文本**数据
- **特点**：
	- 单引号`‘’`或者双引号`""`均可表示字符串，推荐使用`''`，将`""`留给`HTML`使用
	- `JS`中字符串是**不可变**的；一旦字符串被创建，就永远无法改变它，要改变某个字符串，首先要销毁原来的字符串，再用新值填充该变量
	- `String`有最大长度`2^53-1`，但此最大长度针对的不是字符个数，是`UTF16`字符串编码

### 5 Number
- **定义**：表示通常意义上的**数字**，包括整数和浮点数
- **特点**：
	- 特殊值：
		- `Number.MAX_VALUE`,`Number.MIN_VALUE`：最大值最小值
		- `NaN`：表示Not a Number，非数字；`isNaN()`：任何不能被转化成数值的值，都会返回`true`
		- `Infinity`, `-Infinity`：无穷大，负无穷大
	- `JS`中有`+0`和`-0`，加法运算中无区别，但是除法运算如不检测可能会得到负无穷大
		- 检测方式：检查`1/x`是`Infinity`还是`-Infinity`
	- 整数的运算基本可以保持精确，但是由于浮点数的定义，小数的运算不一定准确
		- 无论是`==`还是`===`都无法用来比较小数
		- 正确比较方法：`Math.abs(0.1 + 0.2 - 0.3) <= Number.EPSILON`
	- 运算：
		- 连字符和加号`+`：如果`+`两边都是数值则进行加法运算，否则算作连字符进行字符串拼接
		- 隐式转化：`-`、`*`、`/`、`%`会自动进行隐式转化（转为数字）`'4' + 2 - 6 = 36`

### 6 Symbol
- **定义**：表示**独一无二**的值
- **特点**：
	- 每个Symbol实例都是独一无二的`Symbol() === Symbol() // return false`

### 7 补充
- **包装对象**：JS中的几个基本类型Number，String，Boolean，Symbol均有包装类
	- 使用new关键字创建：`var n = new Number(3)`
	- 使用`typeof`测试类型为`object`，所以`3 === new Number(3)`返回`false`(`==`返回`true`)
	- 构造器为两用的，搭配`new`时为创建对象(Symbol除外)；直接调用时，表示强制类型转换
	- **基础类型上可以调用其对应包装类的方法**：`.`提供了自动装箱操作`"abc".charAt(0)`

- **常用类型转换**：
	- ToNumber：
		- `Number(num)`：（优先使用）
			- 支持十进制，二进制，八进制和十六进制，如`30`, `0b111`, `0o13`, `0xFF`
			- 支持科学计数法`1e3`，`-1e-2`
		- `parseInt(num, mode)`，`parseFloat(num)`：
			- 分别解析整数和浮点数，解析浮点数时无mode参数，只能解析10进制
			- 通过第二个参数设置进制，如`parseInt("AF", 16)`
			- 不传第二个参数时，只支持16进制前缀，且不支持科学计数法
	- ToString:
		- `String(any)`：转换任意类型至`string`
		- `num + ""`：针对数字
