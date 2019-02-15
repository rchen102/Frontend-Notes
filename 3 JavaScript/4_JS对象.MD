## 4_JS对象
- 内置对象：由ES标准中定义的对象，Math、String、Number、Boolean、Function、Object
- 宿主对象：由JS的运行环境提供的对象，主要指由浏览器提供的对象，BOM、DOM
- 自定义对象：自主创建的对象

### 1 基础说明
- **定义**：
	- 属性的集合
	- key-value组成的无序集合，key可以为字符串或者`Symbol`

- **属性**：
	- 定义：数据属性和访问器属性，本质都是字符串，只不过值可以取任意类型
	- 添加和访问：
		- 通过`.`：对象.属性名，如`stu.name`，`stu.study()`
		- 通过`[]`：对象["属性名"]，如`stu['123']`，用于特殊属性名
	- 删除：
		- 通过`delete`删除：`delete obj.name;`
	- `in`运算符：检测属性是否存在`console.log('name' in stu)`

- **创建**：
	- 使用`new`关键词
	- 对象字面量方式
		- 属性之间`,`隔开，
		- 最后一个属性末尾不加`,`否则有的浏览器（如低版本的IE）将报错

- **遍历**：`for (let n in 对象)`，n遍历属性，可用`obj[n]`来取得属性值

### 2 创建

- **对象字面量**：
	- 优点：简易直观
	- 缺点：不适合大规模重复创建对象

	```javascript
	let person={
	　　name:"小米",
	　　age:23
	};
	```

- **工厂模式**：
	- 优点：解决了创建多个相似对象问题
	- 缺点：类型均为`Object`，没有解决类型标识的问题

	```javascript
	function createPerson(name){   // 一般首字母小写
		let obj=new Object(); // 原料
	    obj.name=name;        // 加工
	    obj.showName=function() {
	       console.log(this.name);
	    }     
	    return obj;   // 出厂
	} 
	let p1=createPerson('小米');
	p1.showName();
	```

- **构造函数**：
	- 优点：解决了类型标识的问题，利用`instanceof`
	- 缺点：每个实例都拥有自己的方法空间，造成空间浪费
	- 特点：构造函数与普通函数并无区别，若不使用关键词`new`，`this`将指向`window`
	- `new`的流程：
		- 开辟内存空间，创建新对象
		- 将新创建的对象设为构造函数中的`this`
		- 执行构造函数中的代码
		- 返回新对象

	```javascript
	function Person(name){ // 一般首字母大写
		this.name=name;
		this.showName=function() {
			console.log(this.name);
		}
	}
	let p1=new Person('小米');
	```

- **原型模式**：
	- 优点：解决了空间浪费问题，拥有共享属性和方法空间（原型详解见后）

	```javascript
	function Person(name){
		this.name=name;
	}
	Person.prototype = {
		showName: function() {
			console.log(this.name);
		}
	}
	let p1=new Person('小米');
	```

### 3 原型(原型对象)/原型链
- **基本概念**：
	- `prototype`：每个构造函数都有一个`prototype`，即**原型对象**（普通函数也有）
	- `__proto__`：每个实例对象都有该属性，并且指向它的**原型对象**（指向构造函数的`prototype`或者`Object`)

- **特点**：
	- 原型对象里的属性`constructor`指向构造函数本身
	- `prototype`对象相当于特点类型所有实例都可以访问的公共容器

- **原型链**：
	- 本质：访问一个对象的属性时，不仅会在对象自身上搜寻，还会搜寻对象的原型，以及对象的原型的原型，直到原型链的末尾
	- 注： `hasOwnProperty('propertyName')`是JS中唯一处理属性不会遍历原型链的方法
	- 作用：实现继承
	```javascript
	function Person(name){ 
		this.name=name;
	}
	Person.prototype.showName = function() { console.log(this.name) }

	// 继承属性
	function Teacher(name, subject) { // 在一个类内执行另外一个类的构造函数，通过call指定this为当前执行环境
		Person.call(this, name);  
		this.subject = subject;
	}
	// 继承方法
	Teacher.prototype = Object.create(Person.prototype); 
	// 不能直接赋值，否则修改Teacher.prototype会影响Person
	// Object.create: 新建一个对象，使用现有对象赋值给新建对象的__proto__
	// let eg = Object.create(ex);  eg.__proto__ = ex;
	Teacher.prototype.constructor = Teacher; // 修正constructor属性
	```