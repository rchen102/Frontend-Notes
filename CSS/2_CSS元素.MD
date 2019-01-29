## 2_CSS元素

### 1 字体属性
```
p{
	font-size:50px; 		/*字体大小*/
	line-height: 30px;      /*行高*/
	font-family:幼圆,黑体; 	/*字体类型：如果没有幼圆就显示黑体，没有黑体就显示默认*/
	font-style:italic;		/*italic表示斜体，normal表示不倾斜*/
	font-weight:bold;	/*粗体：属性值写成bolder也可以*/
	font-variant:small-caps;  /*小写变大写*/
}
```
- **行高**：
	- 盒子模型的padding，不是直接作用在文字上的，而是作用在“行”上的
	- 行高可以用百分比，表示字号的百分之多少
- **字体**：
	- 缺省字体用`,`隔开，浏览器会按顺序匹配
	- 接上，英语字体应放在最前面，这样所有的中文，就不能匹配英语字体，自动匹配后面的中文字体


### 2 文本属性
 - `letter-spacing: 0.5cm ;`  单个字母之间的间距
 - `word-spacing: 1cm;`   单词之间的间距
 - `text-decoration: none;` 字体修饰：none去掉下划线、underline下划线、line-through中划线、overline上划线、
 - `text-transform: lowercase;`  uppercase大写、lowercase小写、capitalize单词首字母大写
 - `color:red;` 字体颜色
 - `text-align: center;` 在当前容器中的对齐方式。属性值可以是：left、right、center（在当前容器的中间）、justify（实现两端对齐文本效果)

### 3 列表属性
- `list-style-image: url(images/eg.jpg)`：将图像设置为列表标记
- `list-style-position: outside`：设置列表项标记的放置位置
- `list-style-type: none`：设置列表项标记的类型


### 4 背景属性
- `background-color:#ff99ff;`  设置元素的背景颜色
- `background-image:url(images/eg.jpg);` 将图像设置为背景
-  `background-repeat: no-repeat;`  设置背景图片是否重复及如何重复，默认平铺满
	- `no-repeat`不要平铺；
	- `repeat-x`横向平铺；
	- `repeat-y`纵向平铺。
- `background-position: center top;` 设置背景图片在当前容器中的位置
	- 单词描述：background-position: 描述左右（left、center、right） 描述上下（top 、center、bottom）
	- 像素值描述：background-position: 向右偏移量 向下偏移量
- `background-attachment: scroll;` 设置背景图片是否跟着滚动条一起移动
	`scroll`（与fixed属性相反，默认属性）、`fixed`（背景就会被固定住，不会被滚动条滚走）
- 简写属性：`background`；作用：将上面的多个属性写在一个声明中