> 偶然看到这篇文章，发现对JavaScript中的细节分析的很到位，读起来非常有趣，遂记录要点如下：


##对象

###对象使用和属性

- JS中所有变量（除了null和undefined）都可以当作对象使用。
- 误解：数字的字面值不能当作对象使用

        2.toString();   //出错：SyntaxError
        //这是JS解析器的一个错误，它试图将点操作符解析为浮点数字面值的一部分
       
        2..toString(); //第二个点号可以正常解析
        2 .toString();/点号前面有空格，可以正常解析
        (2).toString(); //2首先被计算，可以正常解析

- 访问属性

     点操作符和中括号操作符均可。

    中括号操作符在以下两种情况依然有效：

       - 动态设置属性（将其赋予一个变量）
       - 属性名不是一个有效的变量名（比如属性名中包含空格，或者属性是JS关键词）

- 删除属性

    唯一方法是使用delete操作符
 
    设置属性为undefined和null仅仅是移除了属性和值的关联

- 属性名的语法

        var test = {
        'case': 'I am a keyword so I must be notated as a string',
        delete: 'I am a keyword too so me' // 出错：SyntaxError
        };

        //对象的属性名可以使用字符串或者普通字符声明；但是若想在较低版本的JS引擎下运行建议使用字符串字面值声明
 

### 原型

### hasOwnProperty函数

  - 判断一个对象是否包含自定义属性而不是原型链上的属性

  - 唯一一个处理属性但是不查找原型链的函数
  - 当hasOwnProperty被作为某对象属性时候该如何正确调用？
 
        var foo = {
        hasOwnProperty: function() {
        return false;
        },
        bar: 'Here be dragons'
        };

        foo.hasOwnProperty('bar'); // 总是返回 false

        // 使用其它对象的 hasOwnProperty，并将其上下文设置为foo
        ({}).hasOwnProperty.call(foo, 'bar'); // true


### for in 循环

   使用 hasOwnProperty 过滤

    var foo = {moo: 2};
    for(var i in foo) {
    if (foo.hasOwnProperty(i)) {
        console.log(i);
    }
    }
 
  
 
##函数

### 函数声明与表达式

  - 命名函数的赋值表达式

    将命名函数赋值给一个变量

        var foo = function bar() {
        bar(); // 正常运行
        }
        bar(); // 出错：ReferenceError
        //bar 函数声明外是不可见的，这是因为我们已经把函数赋值给了 foo；
        // 然而在 bar 内部依然可见。这是由于 JavaScript 的 命名处理 所致， 函数名在函数内总是可见的。   

- this 的工作原理

     JavaScript 有一套完全不同于其它语言的对 this 的处理机制。 在五种不同的情况下 ，this 指向的各不相同。

      - 全局范围内

            this;
            //当在全部范围内使用 this，它将会指向全局对象。


    - 函数调用

            foo();
            //这里 this 也会指向全局对象。
            //ES5 注意: 在严格模式下（strict mode），不存在全局变量。 这种情况下 this 将会是 undefined。
    - 方法调用
·
              test.foo(); 
             //这个例子中，this 指向 test 对象。

    - 调用构造函数

            new foo(); 
            //如果函数倾向于和 new 关键词一块使用，则我们称这个函数是 构造函数。 在函数内部，this 指向新创建的对象。

     - 显式的设置 this

            function foo(a, b, c) {}

            var bar = {};
            foo.apply(bar, [1, 2, 3]); // 数组将会被扩展，如下所示
            foo.call(bar, 1, 2, 3); // 传递到foo的参数是：a = 1, b = 2, c = 3
            //当使用 Function.prototype 上的 call 或者 apply 方法时，函数内的 this 将会被 显式设置为函数调用的第一个参数。
            //因此函数调用的规则在上例中已经不适用了，在foo 函数内 this 被设置成了 bar。


      - 常见误解

           直接调用函数时，this 指向全局对象被认为是JavaScript语言另一个错误设计的地方，因为它从来就没有实际的用途。

            Foo.method = function() {
            function test() {
            // this 将会被设置为全局对象（译者注：浏览器环境中也就是 window 对象）
            }
            test();
            }
          - 一个常见的误解是 test 中的 this 将会指向 Foo 对象，实际上不是这样子的。

            为了在 test 中获取对 Foo 对象的引用，我们需要在 method 函数内部创建一个局部变量指向 Foo 对象。

                Foo.method = function() {
                var that = this;
                function test() {
                // 使用 that 来指向 Foo 对象
                }
                test();
                }
             that 只是我们随意起的名字，不过这个名字被广泛的用来指向外部的 this 对象。 在 闭包 一节，我们可以看到 that 可以作为参数传递。

        -  方法的赋值表达式

            另一个看起来奇怪的地方是函数别名，也就是将一个方法赋值给一个变量。

                var test = someObject.methodTest;
                test();
          上例中，test 就像一个普通的函数被调用；因此，函数内的 this 将不再被指向到 someObject 对象。

            虽然 this 的晚绑定特性似乎并不友好，但这确实是基于原型继承赖以生存的土壤。

                function Foo() {}
                Foo.prototype.method = function() {};

                function Bar() {}
                Bar.prototype = Foo.prototype;

                new Bar().method();
            当 method 被调用时，this 将会指向 Bar 的实例对象。