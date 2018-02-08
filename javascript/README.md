# JavaScript

*A mostly reasonable approach to JavaScript*

> **Note**: 。


## Table of Contents

  1. [this](#this)

## this

  <a name="this--new"></a><a name="1.1"></a>
  - [1.1](#this--new) `function()` vs `new function()`
    
    ```javascript
    function f1() {
        this.name = 'Tom';
        const that = this;
        f2(that);
    }
    
    function f2(that) {
        this.name = 'Jerry';
        console.log(that.name); //Tom
        console.log(this.name); //Jerry
    }
    ```
    两种执行情况：
    ```javascript
    f1();     //普通函数
    //Jerry
    //Jerry
    
    new f1(); //构造函数
    //Tom
    //Jerry
    ```
    `f1()`作为普通函数执行时，函数内部`this`此时指向`global`,
    而`f2()`未指定调用者，函数内`this`也指向`global`，两者**context**相同。
    `f1()`作为构造函数时，会建立一个独立的**context**，而`f2()`的**context**
    保持不变。


#### 1. 引用

`const`	不可变

`let` 	可变


#### 2. 对象

```javascript
// bad
const item = new Object();

// good
const item = {};
```


#### 3. 创建有动态属性名的对象时，使用可被计算的属性名称

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

#### 4. 使用拓展运算符 ... 复制数组

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

#### 5. 使用解构存取和使用多属性对象

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

#### 6. 对数组使用解构赋值

```javascript
const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;
```


#### 7. 字符串超过 80 个字节应该使用字符串连接号换行

推荐使用 `+` 连接，性能优于 `\`.


#### 8. 程序化生成字符串时，使用模板字符串代替字符串连接

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

#### `class`

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

#### `extemds`

```javascript

// good
class PeekableQueue extends Queue {
  peek() {
    return this._queue[0];
  }
}
```

#### 返回`this`来帮助链式调用

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

#### 命名的函数表达式的变量名会被提升，但函数名和函数函数内容并不会

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

#### 函数声明的名称和函数体都会被提升

```javascript
function example() {
  superPower(); // => Flying

  function superPower() {
    console.log('Flying');
  }
}
```

#### 条件表达式例如 if 语句通过抽象方法 ToBoolean 强制计算它们的表达式并且总是遵守下面的规则

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

#### 使用 /** ... */ 作为多行注释。包含描述、指定所有参数和返回值的类型和值

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

#### 使用 `//` 作为单行注释。在评论对象上面另起一行使用单行注释。在注释前插入空行

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

#### `FIXME` `TODO` `XXX`

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

#### 增加结尾的逗号: 需要

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

#### 使用分号

```javascript

// good (防止函数在两个 IIFE 合并时被当成一个参数)
;(() => {
  const name = 'Skywalker';
  return name;
})();
```

#### 类型转换

```javascript
// bad
const totalScore = this.reviewScore + '';

// good
const totalScore = String(this.reviewScore);
```

#### 位操作符转换

```javascript
// good
/**
 * 使用 parseInt 导致我的程序变慢，
 * 改成使用位操作转换数字快多了。
 */
const val = inputValue >> 0;
```


#### 不使用loop循环，创建一个长度为100的数组，并且每个元素的值等于它的下标
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

#### 布尔
```javascript
// good
const hasAge = Boolean(age);

// good
const hasAge = !!age;
```

#### 使用帕斯卡式命名构造函数或类

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


#### 使用下划线 `_` 开头命名私有属性

```javascript
// bad
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';

// good
this._firstName = 'Panda';
```

#### 别保存 this 的引用。使用箭头函数或 Function#bind

```javascript
// good
function foo() {
  return () => {
    console.log(this);
  };
}
```

####  创建 `get()` 和 `set()` 函数是可以的，但要保持一致

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

#### 使用 $ 作为存储 jQuery 对象的变量名前缀

```javascript
// bad
const sidebar = $('.sidebar');

// good
const $sidebar = $('.sidebar');
```

#### 使用 $ 作为存储 jQuery 对象的变量名前缀

```javascript
// good
const $sidebar = $('.sidebar');
```

#### 对有作用域的 jQuery 对象查询使用 `find`

```javascript
// good
$('.sidebar ul').hide();

// good
$('.sidebar > ul').hide();

// good
$sidebar.find('ul').hide();
```
