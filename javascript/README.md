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
    > `f1()`作为普通函数执行时，函数内部`this`此时指向`global`,
    而`f2()`未指定调用者，函数内`this`也指向`global`，两者**context**相同。
    `f1()`作为构造函数时，会建立一个独立的**context**，而`f2()`的**context**
    保持不变。
