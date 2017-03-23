## March 14, 2017

```javascript
// Set the location property to navigate to a new web page
window.location = "http://www.oreilly.com/";
```

In **client-side JavaScript**, the **Window** object is also the **global** object.

小问题能用原生JavaScript解决的勿用框架，操作更灵活。

## March 15, 2017

### 替换和非替换元素

	**替换元素**：用来替换元素内容的部分不是由文档内容直接显示。例如：`<img>`。

	**非替换元素**：其内容由用户代理（浏览器）在元素本身生成的框中显示。包括大部分`HTML`和`XHTML`，
	例如：`<span>hi there</span>`

### 元素显示角色

	**块级元素**：生成一个元素框，默认填充父级元素的内容区。例如：`<div></div>`和`<p></p>`
	**行内元素**：在一个文本行内生成元素框，不会打断这行文本。例如：<a></a>

	CSS属性 display ： inline 和 block

	```html
	<book>
		<maintitle>Cascading Style Sheets: The Definitive Guide</maintitle>
		<subtitle>Second Edition</subtitle>
		<author>Eric A. Meyer</author>
		<publisher>O'Reilly and Associates</publisher>
		<pubdate>2004</pubdate>
		<isbn>blajblahblah</isbn>
	</book>
	<book>
		<maintitle>CSS2 Pocket Reference</maintitle>
		<author>Eric A. Meyer</author>
		<publisher>O'Reilly and Associates</publisher>
		<pubdate>2004</pubdate>
		<isbn>Tony</isbn>
	</book>
	<style>
	book, maititle, subtitle, author, isbn {display: block;}
	publisher, pubdate {display: inline;}
	</style>
	```


### 属性选择器

  + `p.warning.help` 匹配class属性包含warning和help的所有p元素

  + `a[href][title]` 选择同时有href和title属性的所有a元素

  + `[foo="bar"]`	选择foo属性值等于"bar"的所有元素

  + `[foo~="bar"]`	选择foo属性值中有"bar"属性的所有元素

  + `[foo^="bar"]`	选择foo属性值以"bar"开头的所有元素

  + `[foo$="bar"]`	选择foo属性值以"bar"结尾的所有元素

  + `[foo*="bar"]`	选择foo属性值包含"bar"子串的所有元素

  + `[foo|="bar"]`	选择foo属性等于`bar`或以`bar-`开头的所有元素
  	可用于匹配图片，例如：
	```css
	img[src|="figure"] {border: 1px solid gray;}
	```
	常用语匹配 语言值


### 选择相邻兄弟元素
```css
h1 + p + div {margin-top: 0;}
```
选择 h1 的兄弟元素中的下一个 p 元素的下一个 div 元素
