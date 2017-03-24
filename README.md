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
Array.from(Array(100).keys())
[...Array(100).keys()]
Object.keys(Array(100).join().split(','))
Object.keys(Array(100).fill(undefined))
Object.keys(Array.apply(null,{length:100}))
Array.prototype.recursion = function(length) {
    if (this.length === length) {
        return this;
    }
    this.push(this.length);
    this.recursion(length);
}
arr = []
arr.recursion(100)
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

