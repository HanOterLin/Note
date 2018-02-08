> **Date**: March 15, 2017

#### 替换和非替换元素

**替换元素**：用来替换元素内容的部分不是由文档内容直接显示。例如：`<img>`。

**非替换元素**：其内容由用户代理（浏览器）在元素本身生成的框中显示。包括大部分`HTML`和`XHTML`，例如：`<span>`

#### 元素显示角色

**块级元素**：生成一个元素框，默认填充父级元素的内容区。例如：`<div>`和`<p>`

**行内元素**：在一个文本行内生成元素框，不会打断这行文本。例如：`<a>`

可由CSS属性 `display` 控制 ： inline 和 block


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

#### 属性选择器

`p.warning.help` 匹配class属性包含warning和help的所有p元素

`a[href][title]` 选择同时有href和title属性的所有a元素

`[foo="bar"]`	选择foo属性值等于"bar"的所有元素

`[foo~="bar"]`	选择foo属性值中有"bar"属性的所有元素

`[foo^="bar"]`	选择foo属性值以"bar"开头的所有元素

`[foo$="bar"]`	选择foo属性值以"bar"结尾的所有元素

`[foo*="bar"]`	选择foo属性值包含"bar"子串的所有元素

`[foo|="bar"]`	选择foo属性等于`bar`或以`bar-`开头的所有元素，可用于匹配图片，例如：
```css
img[src|="figure"] {border: 1px solid gray;}
```

#### 选择相邻兄弟元素
```css
h1 + p + div {margin-top: 0;}
```
选择 h1 的兄弟元素中的下一个 p 元素的下一个 div 元素

> **Date**: March 17, 2017

#### `data-*` 的读取和添加

```html
<h1 id="first" data-hehe="Davi" alt="aa kk" >1</h1>

<script type="text/javascript">
	var head = document.getElementsByTagName('first');
	head.dataset	//{hehe : 'Davi'}
	head.dataset.haha = 'huhu'	//add data-* : data-haha="huhu"
</script>
```

#### 静态伪类

```css
a:link {color: purple}

a:visited {color: silver}
```


#### 动态伪类

```css
a:focus		/* when mouse point focus on tag. */
a:hover		/* when mouse point over tag. */
a:active	/* when mouse click tag. */
```

> **Date**: March 20, 2017

#### 1. The first child of the parent element

```css
h1:first-child { background-color: yellow; }
```

#### 2. According to language selection

```html
<p lang="fr">111111</p>
<p lang="en">111111</p>
<p lang="ge">111111</p>
```
```css
h1:lang(ge){ background-color: yellow; }
h1:lang(en){ background-color: red; }
h1:lang(fr){ background-color: blue; }
```

#### 3. 伪元素选择器

设置 **块** 级元素首字母样式

```css
p:first-letter { color: red; }
```

设置 **块** 级元素中的第一个文本行

```css
p:first-line { color: purple; }
```

伪元素必须放在该伪元素选择器的最后面，`p:first-line em` 不合法！

设置 **之前** 和 **之后** 样式

```css
h1:before { content: "台词："; color: yellow; }
h1:after { content: "END"; color: yellow; }
```

#### 4. 不管怎样，无论问题看上去多抽象，多难懂，都要继续努力！你的努力不会白费。

#### 5. 选择器特殊性（优先级）

`id:` 			0, 1, 0, 0.

`class`属性，**属性选择**或**伪类**：	0, 0, 1, 0.

**元素**和**伪元素**：				0, 0, 0, 1.

**结合符** 和 **通配符** 无贡献。


> **Date**: March 25, 2017

#### `! important`

`! important` 重要声明组 高于 非重要声明组

声明冲突时，会将声明非为 `! important` 组，和 `其它`组，并进行组内对比。

```html
<head>
<style type="text/css">
  #rr {
      background-color: red ! important;
    }
</style>
</head>
<body oo="ll">
<h1 id="rr" style="background-color: blue" >结果为 red ,! important 凌驾所有非重要声明组选择器之上</h1>
```

#### 伪类样式顺序 **link-visited-hover-active** **(LVHA)**

```css
a:link {color: black;}
a:visited {color: purple;}
a:hover {color: red;}
a:active {color: orange;}
```

#### 串连伪类

通过将伪类链接在一起，可以缓解特殊性和顺序问题

```css
:link:hover:active {color: orange;}
:visited:hover:active {color: silver;}
```

#### `em` 和 `ex`

`em` 为该元素的`font-size` 的像素长度，不同`font-size`的元素的`em`不同。

`ex` 为该元素字体小写字母`x`的高度，不同字体`ex`不同。

#### `inherit`

继承元素的样式属性

```css
h1:first-child {
  font-size: inherit;
}
```