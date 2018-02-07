## Table of Contents

  1. [this](#this)

## this

  <a name="types--primitives"></a><a name="1.1"></a>
  - [1.1](#types--primitives) `function()`与`new function()`

    ```javascript
    function f1() {
        this.name = 'Tom';
        const that = this;
        f2(that);
    }
    
    function f2(that) {
        this.name = 'Jerry';
        console.log(that.name); //Jerry
        console.log(this.name); //Jerry
    }
    
    f1();
    ```
    
    ```javascript
    
    function func1() {
        this.name = 'Tom';
        const that = this;
        func2(that);
    }
    
    function func2(that) {
        this.name = 'Jerry';
        console.log(that.name); //Tom
        console.log(this.name); //Jerry
    }
    
    new func1();
    ```
// 为什么console.log(that.boy);
// 输出的不是abc？

// 因为这是普通函数，不是构造函数。如果最后一行改成 new abc()，那么执行出来的结果就和你的预期一样了。
// 构造函数建立了一个独立的context，this指向这个context，普通函数的context就是global对象，在浏览器环境下也同指向window这个对象。
// 所以两个函数的this.body都指向global下面的body，你的代码加一行alert(window.boy);然后分别执行abc() 和new abc()，你就清楚区别了
