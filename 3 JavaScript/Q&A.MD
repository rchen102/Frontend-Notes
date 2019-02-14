### 需要特别注意`==`和`===`比较：
 `==`比较，它会自动转换数据类型再比较，很多时候，会得到非常诡异的结果；
 `===`比较，它不会自动转换数据类型，如果数据类型不一致，返回false，如果一致，再比较.

### NaN这个特殊的Number与所有其他值都不相等，包括它自己：
    ```javascript
    NaN === NaN; // false
    isNaN(NaN); // true
    ```

### `this`
- 以函数的形式调用时，this永远都是window。比如fun();相当于window.fun();
- 以方法的形式调用时，this是调用方法的那个对象
- 以构造函数的形式调用时，this是新创建的那个对象

### JS的垃圾回收机制
程序运行过程中会产生垃圾，这些垃圾积攒过多以后，会导致程序运行的速度过慢。所以我们需要一个垃圾回收的机制，来处理程序运行过程中产生垃圾。

当一个对象没有任何的变量或属性对它进行引用时，此时我们将永远无法操作该对象，此时这种对象就是一个垃圾，这种对象过多会占用大量的内存空间，导致程序运行变慢，所以这种垃圾必须进行清理。

上面这句话，也可以这样理解：如果堆内存中的对象，没有任何变量指向它时，这个堆内存里的对象就会成为垃圾。

JS拥有自动的垃圾回收机制，会自动将这些垃圾对象从内存中销毁。我们不需要也不能进行垃圾回收的操作。我们仅仅需要做的是：如果你不再使用该对象，那么，将改对象的引用设置为 null 即可。

#### for循环
`for ... of`
`for ... in`

### 自动加分号问题
```javascript
function foo() {
    return; // 自动添加了分号，相当于return undefined;
        { name: 'foo' }; // 这行语句已经没法执行到了
}
function foo() {
    return { // 这里不会自动加分号，因为{表示语句尚未结束
        name: 'foo'
    };
}
```

###  var & let & const
JS允许直接声明变量，但是这样声明的变量是**全局变量**，不同JS文件中的变量会相互影响
而用`var`声明的变量则**不是全局变量**

由于JavaScript的变量作用域实际上是函数内部，我们在for循环等语句块中是无法定义具有局部作用域的变量的,为了解决块级作用域，ES6引入了新的关键字let，用let替代var可以申明一个块级作用域的变量：
```javascript
function foo() {
    for (var i=0; i<100; i++) {
        //
    }
    i += 100; // 仍然可以引用变量i
}
function foo() {
    var sum = 0;
    for (let i=0; i<100; i++) {
        sum += i;
    }
    // SyntaxError:
    i += 1;
}
```

### 变量提升
JavaScript的函数定义有个特点，它会先扫描整个函数体的语句，把所有申明的变量“提升”到函数顶部
JavaScript引擎自动提升了变量y的**声明**，但不会提升变量y的**赋值**。
```
'use strict';
function foo() {
    var x = 'Hello, ' + y;
    console.log(x);
    var y = 'Bob';
}
foo();  // 不会报错，但是console.log显示Hello, undefined
```

### 命名空间
全局变量会绑定到window上，不同的JavaScript文件如果使用了相同的全局变量，或者定义了相同名字的顶层函数，都会造成命名冲突，并且很难被发现。
减少冲突的一个方法是把自己的所有变量和函数全部绑定到一个全局变量中。例如：
```javascript
// 唯一的全局变量MYAPP:
var MYAPP = {};

// 其他变量:
MYAPP.name = 'myapp';
MYAPP.version = 1.0;
```

### void
- 使用：无论void后的表达式是什么，void操作符都会返回undefined
- 作用：
    - 通过采用`void 0`取`undefined`比采用字面上的undefined更靠谱更安全，应优先使用void 0
    - 填充`<a>`的`href`确保点击时不会产生页面跳转; 填充`<image>`的`src`，确保不会向服务器发出垃圾请求
        - `href="javascript:void(0)"`