## 2_JS语法
- 少数需要注意的语法知识

### 1 `==`和`===`比较：
 `==`比较，它会自动转换数据类型再比较，规则复杂，很多时候，会得到非常诡异的结果
 `===`比较，它不会自动转换数据类型，如果数据类型不一致，返回false，如果一致，再比较

### 2 自动加分号问题
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

### 3 关键词this
- 普通函数：`this`为window
- 对象方法：`this`为调用方法的对象
- 构造函数：`this`为新创建的对象
- call和apply：`this`为指定的对象

### 4 函数
- 立即执行函数
```
(function(a,b) {
	return a+b;
})(1,3);
```
- 声明提前，使用函数声明创建的函数会被提前声明，函数表达式则不能
```
function sum(a, b) {}         // 声明提前
let sum = function(a, b) {};  // 不会提前
```

