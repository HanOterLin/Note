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

**非替换元素**：其内容由用户代理（浏览器）在元素本身生成的框中显示。包括大部分`HTML`和`XHTML`，例如：`<span>`

### 元素显示角色

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

### 属性选择器

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

### 选择相邻兄弟元素
```css
h1 + p + div {margin-top: 0;}
```
选择 h1 的兄弟元素中的下一个 p 元素的下一个 div 元素

## March 17, 2017

### `data-*` 的读取和添加

```html
<h1 id="first" data-hehe="Davi" alt="aa kk" >1</h1>

<script type="text/javascript">
	var head = document.getElementsByTagName('first');
	head.dataset	//{hehe : 'Davi'}
	head.dataset.haha = 'huhu'	//add data-* : data-haha="huhu"
</script>
```

### 静态伪类

```css
a:link {color: purple}

a:visited {color: silver}
```


### 动态伪类

```css
a:focus		/* when mouse point focus on tag. */
a:hover		/* when mouse point over tag. */
a:active	/* when mouse click tag. */
```

## March 20, 2017

### 1. The first child of the parent element

```css
h1:first-child { background-color: yellow; }
```

### 2. According to language selection

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

### 3. 伪元素选择器

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

### 4. 不管怎样，无论问题看上去多抽象，多难懂，都要继续努力！你的努力不会白费。

### 5. 选择器特殊性（优先级）

`id:` 			0, 1, 0, 0.

`class`属性，**属性选择**或**伪类**：	0, 0, 1, 0.

**元素**和**伪元素**：				0, 0, 0, 1.

**结合符** 和 **通配符** 无贡献。


## March 22, 2017

### 1. 引用

`const`	不可变

`let` 	可变


### 2. 对象

```javascript
// bad
const item = new Object();

// good
const item = {};
```


### 3. 创建有动态属性名的对象时，使用可被计算的属性名称

```javascript
function getKey(k) {
  return `a key named ${k}`;
}

// bad
const obj = {
  id: 5,
  name: 'San Francisco',
};
obj[getKey('enabled')] = true;

// good
const obj = {
  id: 5,
  name: 'San Francisco',
  [getKey('enabled')]: true,
};
```

### 4. 使用拓展运算符 ... 复制数组

```javascript
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
```

### 5. 使用解构存取和使用多属性对象

```javascript
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}

// good
function getFullName(obj) {
  const { firstName, lastName } = obj;
  return `${firstName} ${lastName}`;
}

// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}
```

### 6. 对数组使用解构赋值

```javascript
const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;
```


### 7. 字符串超过 80 个字节应该使用字符串连接号换行

推荐使用 `+` 连接，性能优于 `\`.


### 8. 程序化生成字符串时，使用模板字符串代替字符串连接

```javascript
// bad
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// bad
function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}

// good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

## March 24, 2017

### `class`

```javascript
class Queue {
  constructor(contents = []) {
    this._queue = [...contents];
  }
  pop() {
    const value = this._queue[0];
    this._queue.splice(0, 1);
    return value;
  }
}
```

### `extemds`

```javascript

// good
class PeekableQueue extends Queue {
  peek() {
    return this._queue[0];
  }
}
```

### 返回`this`来帮助链式调用

```javascript
class Jedi {
  jump() {
    this.jumping = true;
    return this;
  }

  setHeight(height) {
    this.height = height;
    return this;
  }
}

const luke = new Jedi();

luke.jump()
  .setHeight(20);
````

### 命名的函数表达式的变量名会被提升，但函数名和函数函数内容并不会

```javascript
function example() {
  console.log(named); // => undefined

  named(); // => TypeError named is not a function

  superPower(); // => ReferenceError superPower is not defined

  var named = function superPower() {
    console.log('Flying');
  };
}
```

### 函数声明的名称和函数体都会被提升

```javascript
function example() {
  superPower(); // => Flying

  function superPower() {
    console.log('Flying');
  }
}
```

### 条件表达式例如 if 语句通过抽象方法 ToBoolean 强制计算它们的表达式并且总是遵守下面的规则

- 对象 被计算为 true
- Undefined 被计算为 false
- Null 被计算为 false
- 布尔值 被计算为 布尔的值
- 数字 如果是 +0、-0、或 NaN 被计算为 false, 否则为 true
- 字符串 如果是空字符串 '' 被计算为 false，否则为 true

```javascript
if ([0]) {
  // true
  // An array is an object, objects evaluate to true
}

if (name) {
  // ...stuff...
}

// good
if (collection.length) {
  // ...stuff...
}
```

### 使用 /** ... */ 作为多行注释。包含描述、指定所有参数和返回值的类型和值

```javascript
// good
/**
 * make() returns a new element
 * based on the passed in tag name
 *
 * @param {String} tag
 * @return {Element} element
 */
function make(tag) {

  // ...stuff...

  return element;
}
```

### 使用 `//` 作为单行注释。在评论对象上面另起一行使用单行注释。在注释前插入空行

```javascript
// good
// is current tab
const active = true;

// good
function getType() {
  console.log('fetching type...');

  // set the default type to 'no type'
  const type = this._type || 'no type';

  return type;
}
```

### `FIXME` `TODO` `XXX`

```javascript
class Calculator {
  constructor() {
    // FIXME: shouldn't use a global here
    total = 0;
  }
}

class Calculator {
  constructor() {
    // TODO: total should be configurable by an options param
    this.total = 0;
  }
}
```

### 增加结尾的逗号: 需要

> 为什么? 这会让 git diffs 更干净。另外，像 babel 这样的转译器会移除结尾多余的逗号，也就是说你不必担心老旧浏览器的尾逗号问题

```javascript

// good - git diff with trailing comma
const hero = {
     firstName: 'Florence',
     lastName: 'Nightingale',
+    inventorOf: ['coxcomb chart', 'modern nursing'],
}

// good
const hero = {
  firstName: 'Dana',
  lastName: 'Scully',
};

const heroes = [
  'Batman',
  'Superman',
];
```

### 使用分号

```javascript

// good (防止函数在两个 IIFE 合并时被当成一个参数)
;(() => {
  const name = 'Skywalker';
  return name;
})();
```

### 类型转换

```javascript
// bad
const totalScore = this.reviewScore + '';

// good
const totalScore = String(this.reviewScore);
```

### 位操作符转换

```javascript
// good
/**
 * 使用 parseInt 导致我的程序变慢，
 * 改成使用位操作转换数字快多了。
 */
const val = inputValue >> 0;
```


### 不使用loop循环，创建一个长度为100的数组，并且每个元素的值等于它的下标
```javascript
Array.from(Array(100).keys());

[...Array(100).keys()];

Object.keys(Array(100).join().split(','));

Object.keys(Array(100).fill(undefined));

Object.keys(Array.apply(null,{length:100}));

Array.prototype.recursion = function(length) {
    if (this.length === length) {
        return this;
    }
    this.push(this.length);
    this.recursion(length);
}
arr = [];
arr.recursion(100);

Array(100).fill(0).map(function (val, index) {
    return index;
})
```

### 布尔
```javascript
// good
const hasAge = Boolean(age);

// good
const hasAge = !!age;
```

### 使用帕斯卡式命名构造函数或类

```javascript
// good
class User {
  constructor(options) {
    this.name = options.name;
  }
}

const good = new User({
  name: 'yup',
});
```


### 使用下划线 `_` 开头命名私有属性

```javascript
// bad
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';

// good
this._firstName = 'Panda';
```

### 别保存 this 的引用。使用箭头函数或 Function#bind

```javascript
// good
function foo() {
  return () => {
    console.log(this);
  };
}
```

###  创建 `get()` 和 `set()` 函数是可以的，但要保持一致

```javascript
class Jedi {
  constructor(options = {}) {
    const lightsaber = options.lightsaber || 'blue';
    this.set('lightsaber', lightsaber);
  }

  set(key, val) {
    this[key] = val;
  }

  get(key) {
    return this[key];
  }
}
```

### 使用 $ 作为存储 jQuery 对象的变量名前缀

```javascript
// bad
const sidebar = $('.sidebar');

// good
const $sidebar = $('.sidebar');
```

### 使用 $ 作为存储 jQuery 对象的变量名前缀

```javascript
// good
const $sidebar = $('.sidebar');
```

### 对有作用域的 jQuery 对象查询使用 `find`

```javascript
// good
$('.sidebar ul').hide();

// good
$('.sidebar > ul').hide();

// good
$sidebar.find('ul').hide();
```

## March 25, 2017

### `! important`

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

### 伪类样式顺序 **link-visited-hover-active** **(LVHA)**

```css
a:link {color: black;}
a:visited {color: purple;}
a:hover {color: red;}
a:active {color: orange;}
```

### 串连伪类

通过将伪类链接在一起，可以缓解特殊性和顺序问题

```css
:link:hover:active {color: orange;}
:visited:hover:active {color: silver;}
```

### `em` 和 `ex`

`em` 为该元素的`font-size` 的像素长度，不同`font-size`的元素的`em`不同。

`ex` 为该元素字体小写字母`x`的高度，不同字体`ex`不同。

### `inherit`

继承元素的样式属性

```css
h1:first-child {
  font-size: inherit;
}
```