## 5_CSS盒子模型
- 盒子的主要属性（标准盒子）:
	- width和height：内容的宽度、高度（非盒子的宽度、高度）
	- padding：内边距
	- border：边框
	- margin：外边距

### 1 padding
- **padding区域有颜色**：background-color将填充所有border以内的区域
- **padding四个方向**：顺时针顺序（上右下左）
	![](http://www.w3school.com.cn/i/ct_css_margin_value.gif)
- **部分元素，默认带有padding**：如`<ul>`不加任何样式有40px的padding-left

### 2 border
- **属性**：像素（粗细）、线型、颜色，如`border:1px solid red;`
- **border属性能够被拆开**：（用小属性层叠大属性）
	- 三要素拆开：border-width、border-style、border-color
	- 方向拆开：border-top、border-right、border-bottom、border-left

### 3 margin
- margin塌陷/margin重叠：
	- **标准文档流**中，竖直方向的margin不叠加，取较大的值作为margin
	- 水平方向的margin是可以叠加的，即水平方向没有塌陷现象
- 盒子居中margin:0 auto;
	- 只有标准流的盒子，才能使用`margin:0 auto;`居中，当一个盒子浮动了、绝对定位了、固定定位了，都不能使用margin:0 auto;
	- 使用`margin:0 auto;`的盒子，必须有width，有明确的width。（可以这样理解，如果没有明确的witdh，那么它的witdh就是霸占整行，没有意义）
	- `margin:0 auto;`是让盒子居中，不是让盒子里的文本居中，文本的居中，要使用`text-align:center;`

### 4 善于使用父亲的padding，而不是儿子的margin
- 如果父亲没有border，那么儿子的margin实际上踹的是“流”，踹的是这“行”，父亲整体也会掉下来
- margin这个属性，本质上描述的是兄弟和兄弟之间的距离； 最好不要用这个marign表达父子之间的距离

### 5 IE盒子和标准盒子的区别
- **标准盒子模型**：width 和 height 指的是content的宽度和高度，增加padding、border和margin不会影响content的尺寸，但是会增加元素框的总尺寸
- **IE盒子模型**：width 和 height 指的是content+padding+border的宽度和高度