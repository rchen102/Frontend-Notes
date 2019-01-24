## 1_CSS基础

### 1 CSS概述
- **定义**：Cascading Style Sheet，层叠样式表
- **作用**：将网页内容和显示样式进行分离，提高了显示功能
- **优点**：数据和显示分开，使开发效率提高了（耦合性降低，一个人负责写html，一个人负责写css

### 2 CSS和HTML的结合方式
- **行内样式**：在某个特定的标签里采用style**属性**。范围只针对此标签
- **内嵌样式表**：在页面的head里采用`<style>`**标签**。范围针对此页面
- **引入外部样式表css文件**的方式。这种方式又分为两种：
	- `<link>`标签`<link rel = "stylesheet" type = "text/css" href = "a.css"></link>`
	- `import`，必须写在`<style>`标签中，并且必须是第一句。例如：`@import url(a.css) ;`
	> 两种引入样式方式的区别：外部样式表中不能写标签,但是可以写import语句