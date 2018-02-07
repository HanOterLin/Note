## Table of Contents

  1. [this](#this)

## this

  <a name="types--primitives"></a><a name="1.1"></a>
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
    两种执行结果差异：
    ```javascript
    f1();     //普通函数
    //Jerry
    //Jerry
    
    new f1(); //构造函数
    //Tom
    //Jerry
    ```
    > **原因**： `f1()`作为普通函数执行时，函数内部`this`此处指向`global`,
    `f2()`亦未指定调用者，**context**默认为`global`，两者**context**相同。
    `f1()`作为构造函数执行时，新建一个独立的**context**，`f2()`仍指向`global`,
    二者`this`指向不同。
