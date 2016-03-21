
# JavaScript高级程序设计（第三版）笔记

 
> 前言：一个月大概读了个七七八八，对于本书知识点有了大体的印象，然而一些更深入的知识却没有完全掌握，故重读此书并加以记录，希望能在重读总结过程中能对知识巩固并加以提升。

### 第一章 JavaScript简介

- 诞生于1995年，当时主要功能：**客户端验证**


- 实现需要三部分
  + **ECMAScript**
  
      宿主环境有：web浏览器 ,Node和Adobe Flash
  + **DOM**
        
      将整个页面映射为一个多层节点结构
  + **BOM**
         
      无BOM标准可以遵循

### 第二章 在HTML中使用JavaScript

- 使用`<script>`元素来插入脚本（可直接将脚本代码写入或链接外域脚本）
   
  + `<script>`元素属性
  
         1.async   异步加载脚本及页面内容（但不保证同时拥有此属性的两个脚本的执行顺序）**只对外部文件有效**
  
         2.charset 表示通过src属性指定的代码的字符集，多数浏览器忽略其值

         3.defer  到文档完全被解析后（遇到</html\>后）脚本再运行（**立即下载，延迟运行**）**只对外部文件有效**

         4.language 已废弃

         5.src   表示外部文件地址（带有src属性的标签会忽略内部嵌入的代码）

         6.type  MIME类型  默认为“text/javascript”
                   
  + `<script>`元素的位置

         传统做法：放在`<head>`标签中  弊端：浏览器遇到<body/>元素才开始呈现页面内容，故所有脚本文件下载解析执行完成后才开始呈现

         建议做法：放在`</body>`前或将其代码包裹于`window.onload=function(){}`中

 + 使用外部文件的好处
 
         可维护性；可缓存（有多个页面共用一个js文件的时候可以加快页面加载速度）；适应未来（兼容XHTML和HTML）                       
                         
- 文档模式（主要影响CSS的执行）

   + 混杂模式（quirks mode）
   
         文档开始处没有文档类型声明或者声明错误，则会触发混杂模式

   + 标准模式（standards mode）
   + 准标准模式（almost standards mode）
   
          通过使用过渡型（transitional）或框架集型（frameset）文档类型来触发

- `<noscript>`元素

         <!--适用于浏览器不支持脚本 或 脚本被禁用 两种情况，正常情况不会显示内容-->
         
	       <noscript>
	     
	      <p>本页面需要浏览器支持（启用）JavaScript</p>
	    
	       </noscript>

### 第三章 基本概念

#### 语法
***
- 区分大小写
- 标识符
 + 第一个字符： 字母或下划线或美元符号$
 + 其他字符还可以是数字
 + 惯例：采用驼峰大小写格式
- 注释

         //单行注释

         /*
          *     多行注释
          *
          */
- 严格模式（strict mode）

         “use strict”; //在顶部添加将JS引擎切换到严格模式

          //或
        
          function doSomething()

          {       "use strict";//仅在此函数下使用严格模式
             
                  //函数体
          }

#### 关键字和保留字  
***
 + 均不能用作标识符
 + 在严格模式和非严格模式下保留字有所增减
 
####变量
***
 -  松散类型（可以用来保存任何类型的数据）
 -  局部变量和全局变量
 
        function test(){
        var message="哈哈"；//定义局部变量
         }
        test(); //执行一次函数
        alert(message);//错误 ，若在函数中定义变量时省略var，则定义了全局变量，此处将不会报错

 - 同时定义多个变量，用逗号分隔

        var me="Chinese" ，
        him=“Japanese”，
        you="Korean"；     

#### 数据类型
***
- Undefined 
      
	    var message;
	    alert(message);//"undefined"
        alert(name);//抛出错误
	    alert（typeof message）；//“undefined”
		alert（typeof name）；“undefined”
        //最好的做法是：每当定义一个变量的时候都应当赋予其初始值，这样当typeof操作符显示“undifined”时，我们就知道这个变量未声明
   
- Null

    	var message=null;
        alert(typeof message);//"object"      null值表示一个空对象指针
        alert（null == undefined;//"true"     undefined派生自null值
        //另外只要意在保存对象的变量还未真正保存对象，则应赋予其null值：一可体现null作为空对象指针的惯例；二可区分null和undefined

- Boolean


 	    /*字面值有true和false两个（注意区分大小写）
         *转型函数Boolean()可以将一个值转换为对应的布尔值
         *转换成false的有：空字符串，0和NaN，null，undefined
         * /
         //流控制语句会自动执行转换，如下：
         var name="zhang san";
         if(name){
 	      alert("yes");      // "yes"
             }
        
- Number

 + 浮点数值
    
        保存浮点数值需要的内存空间是保存整数值的两倍，故在ECMAScript中会尽量将浮点数转换为整数值
        
         尽量不要用浮点数值进行比较
  
 + 数值范围
   
         可以使用`isFinite（）`来判断是否无穷，不是则返回true      
 + NaN  

         任何涉及NaN的操作都会返回NaN；

         NaN与任何值都不相等，包括自身。

         可以调用`isNaN（）`函数来确定该数值是不是NaN

        `isNaN（）`也适用于对象，首先调用对象的`valueOf（）`方法，然后确定返回值能否转换为数值，若不能，基于返回值调用`toString（）`方法，再测试返回值

 + 数值转换

         `Number（）`

         可以用于任何数据类型（null值返回0，undefined值返回NaN，对象的话先调用`valueOf（）`，若返回NaN，则调用`toString()`

         `parseInt()`
   
         专用于将字符串转换为数值

         从第一个开始解析，若为数字则继续，直到遇见非数值，然后输出

         空字符串则返回NaN

        可识别十六进制八进制，故可以为该函数提供第二个参数，指定按照哪一种进制进行解析

         `parseFloat（）`

         可解析第一个小数点，之后的小数点无效；

         始终忽略前导的0（只解析十进制值）；

         若字符串包含的是一个可以解析为整数的数（无小数点或小数点后全为0），则输出整数
        
- String

       + 双引号和单引号都ok
       +  ECMAScript中字符串一旦创建则值不能改变，故要赋予一个变量新的字符串值，则需要将原来的销毁，再用新的填充
       +  `toString（）`
           
        除了null和undefined值之外都有`toString（）`方法

        调用数值的时候可以传入转换进制数的参数，如下：(不传参默认十进制)

              var num=10；
              alert（num.toString(8)）;//  "12"

         还有`String()`方法，相当于对`toString（）`方法的扩展，在null和undefined值时返回“null”和“undefined”

- Object

     + Object类型是所有它的实例的基础---其所具有的任何属性和方法也存在于实例中
        
#### 操作符
***
- 一元操作符

  + 递增和递减操作符（++ 和 --）

         有前置型和后置型两种

         前置时先进行加减再求值，后置则是先求值再加减

  + 一元加和减操作符（+ 和 -）

         对非数值操作时会先用Number（）进行转换

- 位操作符

       用于在最底层按内存中表示数值的位来操作数值

       ECMAScript中所有数值都以IEEE-754  64位格式存储，由于位操作符不能操作64位值，故先将其转换为32位，然后执行操作，最后将结果转换为64位。

       有符号整数中，32位中的前31位用于表示整数的值，第32位表示数值符号（0 正 1 负）

       正数以纯二进制存储；

       负数使用二进制补码存储：1.求该数值绝对值的二进制码；2.反码并加1

        var num= - 8;
        alert(num.toString(2));   //  "-1000"     更合乎逻辑的形式

       对NaN和Infinity值应用位操作符时，都会被当成0处理

      + 按位非  ～

         结果就是返回数值的反码，实质是操作数负值再减一

      +  按位与  &
                  
         将二进制码对齐，对应位均为1时返回1，其余均为0      

      + 按位或  |
      
         只要对齐位有1则返回1，只有均为0时才返回0  

      + 按位异或  ^
      
         对齐位上只有一个1时返回1，其余情况均返回0       

      + 左移 <<
      
         会将数值的所有位向左移动（符号位不受影响），空出来的位用0补      

      + 有符号右移 >>
      
         将数值向右移动（符号位不受影响），空出来的位用0补

      + 无符号右移 >>>
      
         符号位受影响        

- 布尔操作符

  + 逻辑非  ！

        同时使用两个逻辑非，即！！，相当于模拟Boolean（）的行为

  +  逻辑与 &&

        不一定返回布尔值（具体见规则）

        属于短路操作，即第一个操作数能决定结果则不会对第二个操作数求值

  + 逻辑或 ||

        不一定返回布尔值

        属于短路操作

              var myObject=preferredObject || backupObject ;   
              //如果pO中值不是null,那么它将被赋给mO；反之则将bO赋给mO

- 乘性操作符

     + 乘法    *
     + 除法  /
     + 求模  %  
     
  
- 加性操作符   

    加法操作符也可以用来连接字符串

- 关系操作符

     比较字符串时，会转化为字符编码进行比较

- 相等操作符

      ==  先转换再比较

      ===  只比较不转换

- 条件操作符

     即三目运算符

        var max=(num1>num2)？num1：num2 ；
        //若num1大于num2，则将num1赋给num，反之将num2赋给num 
   
- 赋值操作符

        num+=1；//类似于num=num+1；

- 逗号操作符

        var num=（5，4，3，2，1）；//num的值为1

      用于声明多个变量，以及赋值（如上）

#### 语句
***
- if语句

     推荐使用代码块（使用花括号包围）

- do-while语句

     至少会执行一次

- while 语句

    有可能永远不会执行

- for语句

    同while循环

- for-in语句

    迭代语句，用来枚举对象的属性

         for（var propName in window）{
                 document.write(propName);     
                     }
          //每个循环将window对象中的某个属性赋给propName，直到所有属性都枚举完毕。

    若要迭代的对象为null或undefined，for-in会抛出错误；

    ECMAScript5更正了该行为，不抛出错误，而是停止执行循环体。

    故建议为保证兼容性，使用该循环前线检测对象是否是null或undefined

- label语句

    lable：statement

    在代码中添加标签以便将来使用，一般是和for语句等循环语句使用（break或者continue调用）

- break和continue语句

    break会立即跳出循环，直接执行循环后面的语句；

    continue只是跳出本层循环，然后从循环顶部继续执行。

        //lable语句与break/continue语句的结合

        var num=0;
        outermost:
        for(var i =0 ; i<10 ;i++){
               for(var  j=0;j<10;j++){
                    if(i==5 && j==5){
                    break outermost; 
                    }
                   num++;
               } 

         }

        alert(num);  //55,若为continue outermost 则为95

- with语句

    with语句的作用是将代码的作用域设置到一个特定的对象中（简化多次编写同一个对象的工作）

        var qs = location.search.substring(1);
        var hostName = location.hostname;
        var url = location.href;

        //以上可以简化为：

        with(location){
        var qs = search.substring(1);
        var hostName = hostname;
        var url = href;
        }
        //在with语句内部，每个变量首先被认为是局部变量，而如果在局部环境中找不到该变量的定义，就会查询location对象中是否有同名属性，若发现了同名属性则将location对象属性的值作为变量的值

- switch 语句

       switch语句在比较值时使用全等操作符

#### 函数
***   
- 参数

  + 为何ECMAScript中函数不介意传入多少参数，也不在乎传入的是什么类型的参数？

        因为在ECMA内部参数是用一个数组来表示的，传入的参数全部在该数组中，可以通过arguments对象来访问这个参数数组，从而获取给函数传的每一个参数

  + arguement对象   

         + 与数组类似，但并不是Array的实例，可以使用方括号语法来访问它的每一个元素
         + 通过访问arguement.length可以获知有几个参数（此长度的值是由传入参数的个数决定的，不是由定义函数时的命名参数个数决定的）
         + arguement可以与命名参数一起使用
         + 未传递值的命名参数将自动被赋予undefined值

- 没有重载

   + 什么是重载

        允许在同一个范围内声明几个功能类似的同名函数，但这些同名函数的形式函数（参数个数，类型或者顺序）必须不同，也就是用同一个运算符完成不同的运算功能

   + 需要什么条件才能实现重载

        为一个函数编写多个定义，只要这多个定义的签名（接收的参数的类型和数量）不同即可

        ECMAScript中函数的参数是由包含多个值的数组实现的，所以其函数没有签名，不能实现重载

  + 那么如果在ECMAScript中定义两个重名的函数会出现什么情况？

        后者会覆盖前者，即起作用的是后者，前者无效

### 第四章 变量，作用域和内存问题

####  基本类型和引用类型的值
***   

   基本类型值：Undefined，Null，Boolean，Number和String， 按值访问。

   引用类型值：保存在内存中的对象（JS不允许直接访问内存中的位置），按引用访问。当复制保存着对象的某个变量时，操作的是对象的引用；但是在为对象添加属性时，操作的是实际对象。

  当我们需要访问引用类型（如对象，数组，函数等）的值时，首先从栈中获得该对象的地址指针，然后再从堆内存中取得所需的数据。

- 动态添加属性

    不能给基本类型值添加属性，不会报错，但是不能访问（undefined）

- 复制变量值

    + 基本类型值变量的复制

        将一个基本类型值变量赋给新变量时，只会创建一个值的副本给新的变量，两者之间无任何联系。

    + 引用类型值变量的复制

        虽然也是副本，但该副本是一个指针，这个指针指向存储在堆中的一个对象

            var obj1= new Object();
            var obj2=obj1;
            obj1.name="one time";
            alert(obj2.name);  // "one time"

- 传递参数

    向参数传递基本类型值时，被传递的值会被复制给一个局部变量-即命名参数（arguement中的一个元素）

    向参数传递引用类型值时，会把这个值在内存中的地址（即指针）复制一份给一个局部变量

    访问变量可以按值访问和按引用访问，而参数只能按值传递。

            function doSomrthing(obj){
                      obj.name="王二"；
                      obj=new Object;
                      obj.name="张三"；
                  }
           var obj1=new Object（）；
           doSomething（obj1）；
           alert（obj1.name）；  //  "王二"

- 检测类型

     instanceof

        alert（person instanceof Object）；
        //根据变量的原型链来识别

####  执行环境及作用域
***      
     
- 执行环境：定义了变量或函数有权访问的其他数据，决定他们的行为；

- 全局执行环境：最外围的执行环境；web浏览器中被认为是window对象，因此所有全局变量和函数都是作为window对象的属性和方法创建的；

- 某个执行环境中的所有代码执行完毕后，该环境被销毁，保存在其中的所有变量和函数定义也随之销毁；但是全局执行环境直到浏览器关闭才会被销毁；

- 变量对象：每个执行环境都有一个关联的变量对象，环境中定义的所有变量和函数都保存在这个对象中

- 活动对象：每进入一个执行环境，该环境中的变量对象就被激活，即为活动对象。活动对象最开始时只包含一个变量，即arguement对象（该对象在全局环境中不存在）

- 当执行流进入一个函数时，函数的环境就会被推入一个环境栈中，在函数执行之后，栈将其环境弹出，把控制权返回给之前的执行环境

- 当代码在一个环境中执行时，会创建变量对象的一个作用域链，保证对执行环境有权访问的所有变量和函数的有序访问。作用域链的前端始终是代码所在环境的变量对象（活动对象），作用域链中下一个变量对象来自包含环境，再下一个来自下一个包含环境，一直延续到全局环境；全局环境中的变量对象始终是作用域链中的最后一个对象。
- 标识符解析式沿着作用域链逐级搜索标识符的过程（若找不到，会导致错误）
- 内部环境可以通过作用域链访问所有外部环境，但是外部环境不能访问内部环境中的任何变量和函数
- 如何延长作用域链？

  + try-catch语句中的catch块
   
        创建一个新的变量对象，其中包含的是被抛出的错误对象的声明
  + with语句

        会将指定的对象添加到作用域中
- JS中没有块级作用域这一说

       if语句，for语句中的变量会添加到执行环境中
  
####  垃圾收集
***      

- 标记清除

    垃圾收集器在运行的时候会将内存中所有的变量全部加上标记，之后去除环境中的变量以及被环境中的变量所引用的变量的标记，剩下的还有标记的变量即被视为准备删除的变量。最后，完成内存清除工作，销毁那些带标记的变量并回收所占用的内存空间。

- 引用计数

    跟踪记录每个值被引用的次数，当该值引用次数变为0时，则可以将其内存空间回收。

    + 循环引用

            function problem(){

            var objA=new Object();
            var objB=new Object();
            objA.someThing=objB;
            objB.otherThing=objA;
            }
            //引用次数永远不能为0   ？？？

      	IE中有一部分对象并不是原生js对象，比如其BOM和DOM中的对象就是使用C++以COM对象的形式实现的，而COM对象的垃圾收集机制采用的就是引用计数策略

           可以使用代码将其设置为null清除引用
       
### 第五章 引用类型

####  Object类型
***     

- 如何创建Object实例
   + 使用new操作符

            var person = new Object（）；
            person.name = "王二"；
            person.sex = "男"； 
   + 使用对象字面量

            var person = {
                name："王二"，
                sex："男"   // 最后一个属性不能添加逗号  
             }
- 访问对象属性的方法

    + 使用点表示法

            alert(person.name);
    + 使用方括号表示法
    
            alert(person["name"]); 
    + 使用方括号表示法的好处：

          + 可以通过变量来访问属性

                var propertyName="name";
                alert(person[peopertyName]);

          + 若属性名中包含会导致语法错误的字符或者属性名是关键字或者保留字，可以使用方括号表示法

                person["first name"]="二"；

####  Array类型
***     
 + ECMAScript中的数组与其他语言的区别：
    + ECMAScript中的数组每一项都可以保存任何类型的数据；
    + ECMAScript数组的大小是可以动态调整的
 + 如何创建数组？
    + 使用Array构造函数
    
            var numbers = new Array();
            var colors = new Array(5);   //传入数量，指定数组的长度，即length的值
            var names = new Array（“Tom”，“Jack”）；//直接传入值
            var values = Array（）；//可以省略new操作符

    + 使用数组字面量表示法

            var names = ["Jack","Tom","Jerry"];
 + 读取和设置数组

     + 使用方括号表示法

            var colors = ["red","green","blue"];
            alert(colors[2]);  //  "blue"

     + 神奇的length属性

         不是只读的！！
  
         通过设置它的值，可以从数组末尾移除或者添加项
+ 检测数组

        if(value instanceof Array){
              //do something
        }
        // 假定只有一个全局执行环境

        if(Array.isArray(value)){
             //do something
        }
        //不论在哪一个全局执行环境中创建都可以判断是不是数组
+ 转换方法

    + toLocaleString（），toString（），valueOf()

        调用toString（）会返回由数组中的每个值的字符串形式拼接而成的一个以逗号分隔的字符串

        调用valueOf（）返回的还是数组

        alert（）要接收字符串参数，所以他会在后台调用toString（）方法

    + join()方法

        接收一个参数，用作分隔符的字符串

            var colors=["blue","green","red"];
            alert(colors.join("|"));    //    blue | green | red 

        不传值或者传undefined，则使用逗号分隔
+ 栈方法

    LIFO（Last In First Out）后进后出

    + `push()`

        接收任意数量的参数添加到数组末尾，并返回修改后数组的长度
    + `pop()`
     
        从数组末尾移除最后一项，并返回移除的项

+ 队列方法

    FIFO（First In First Out）先进先出

    + ` shift（）`
      
        移除数组中的一个项 ，并返回该项

   + `unshift（）`

        能在数组前段添加任意多个参数并返回修改后的长度

+ 重排序方法

   + `reverse()`
 
        反转数组项的顺序
   + `sort（）`

        默认情况下，会调用每个数组项的toString（）方法，然后比较字符串结果按照升序排列数组

        默认情况一般不符合预期，可以向数组中传入比较函数名，按照该函数的规则排序

+ 操作方法
   
   + `concat（）`

        创建一个数组副本，并将接收到的参数添加到该副本的末尾

  + `slice（）`

        接收两个参数，起始位置和结束位置（如果只有一个参数，则默认从开始位置一直到数组末尾）

        然后创建一份该范围内的数组副本

        如果参数中有负数，则用数组长度加上该数来确定位置；若结束位置小于起始位置或者仍然为负数，则返回空数组
        
   + `splice（）`     

         + 删除  指定两个参数：要删除的第一项的位置和要删的项数
         + 替换（插入）   指定三个参数：起始位置，要删除的项数，要插入的项

+ 位置方法

  + `indexOf（）`

        接收两个参数，要查找的项和查找起点位置（可选），从头到尾顺序查找；

        返回查找的项在数组中的位置，没有的话返回-1；

        在比较的一个参数和数组中的每一个项的时候使用的是全等操作符
  + `lastIndexOf（）`

        与上面的方法相似，只是查找顺序是从尾到头

+ 迭代方法

  + `every（）`

        对数组中每一项都运行给定函数，若每一项都返回true，则返回true

  + `some（）`

        对数组中每一项都运行给定函数，只要有一项返回true，则返回true

  + `filter（）`
  
        对数组中每一项都运行给定函数，返回该函数会返回true的项组成的数组

  + `forEach（）` 

        对数组中每一项都运行给定函数，无返回值

  + `
  + （）`

        对数组中每一项运行给定函数，返回每次函数调用结果组成的数组

+ 归并方法

  + `reduce()`

        从数组第一项开始，逐个遍历

        接收两个参数，在每一项调用的函数和作为归并基础的初始值；

        作为调用函数，接收四个参数，前一个值，当前值，项的索引和数组对象，这个函数返回的任何值都会作为的一个参数传给下一项
   + `reduceRight（）`

         与上类似，方向从末尾开始遍历

####  Date类型
***     
   
ECMAScript中的Date类型是在早期Java中的java.util.Date类基础上创建的，所以Date类型使用自UTC（国际协调时间）1970年1月1日午夜（零时）开始经过的毫秒数来保存日期，可精确到1970年1月1日之前或之后的一亿年。

- 如何创建Date对象

        var now = new Date();
        /*不传参则自动获得当前日期和时间
         *若想传入参数，必须是毫秒数（从UTC1970年1月1日至该日期止经过的毫秒数）
- `Date.parse()` 

    可以将日期转化为毫秒数

    若传入的字符串不能表示日期会返回NaN

        var someDate=new Date("May 25,2011");
        //直接将表示日期的字符串传给Date构造函数，会在后台调用Date.parse（）

- `Date.UTC()`

    同样返回毫秒数

    参数：年份，基于0的月份（一月份是0），月中的哪一天（1-31），小时数（0-23），分钟，秒和毫秒数

       + 只有年份和月份是必须的，若没有提供月中天数，则假设天数为1；若省略其他参数，则全部设为0 

    也可以按照这个格式传入构造函数中，在后台自动调用`Date.UTC()`

- 方法

   + `toLocaleString（）`

        返回与设置的地区相适应格式的日期和时间，包含AM或PM，但不包含地区信息

  + `toString（）`
 
        返回带有时区信息的日期和时间

  + ` valueOf（）`

        返回日期的毫秒表示

####  RegExp类型
***

- 如何创建正则表达式

        var expression = / pattern / flags;
         /* pattern 部分是正则表达式；
          * flags为模式标志：g(global);i (不区分大小写) ；m（多行模式，到达一行文本末尾时继续查找下一行中是否存在）
          * /    

**暂放，待补充正则表达式知识**

####  Function类型
***

每个函数都是Function类型的实例

- 如何创建函数对象

        var sum = function(num1,num2){
           //do something
        };

        var sum = new Function("num1","num2","do something"); // 不推荐

    第二种方法会导致解析两次代码（第一次是解析常规ECMAScript代码，第二次是解析传入构造函数中的字符串）

- 没有重载

    函数名是指针，因此创建同名函数时，后面的会覆盖前面的

- 函数声明与函数表达式

    解析器会首先读取函数声明，使其在执行代码前可用（可访问）；
  
    至于函数表达式，则必须等到解析器执行到它所在的代码行，才会被解释执行。

        alert(sum(10,10));   //"20"
        function sum(num1,num2){
                   return sum1 + sum2; 
        }
      
        alert(sum(10,10));  //报错
        var sum=function(num1,num2){
                   return sum1 + sum2;
        };
       
- 函数内部属性

  + arguments对象

        保存函数参数

        arguments对象有一个callee属性，该属性是一个指针，指向拥有该arguments对象的函数，合理运用可以消除紧密耦合现象

            function  factorial(num) {
              if(num<=1){
                 return 1;     
                }else{
                 return num*arguements.callee(num-1)   // 这里用arguements.callee替代了factorial ，消除了紧密耦合
                 }
               }
  + this 对象

        this对象引用的是函数执行的环境对象

  + caller属性

        该属性中保存着调用当前函数的函数的引用

- 函数属性和方法

   - length属性

        表示希望接收的命名参数的个数

        而arguements.length表示的是实际传入参数的个数

  - prototype属性

        保存所有实例方法的真正所在

        不可以枚举

  - `apply()`方法

        接收两个参数：作用域；参数数组（例：arguments或者[1,2,3]）
  - `call()`方法

        接收两个参数：作用域；参数（必须全部都列出来）

  - `bind()`方法

        接收一个参数，绑定作用域

            window.color = "red";
            var o = { color : "blue"};
            function sayColor(){
                      alert(this.color);
            }
            var objectSayColor = sayColor.bind(o);
            objectSayColor();   // "blue"

   - 继承的`toString()`   `toLocaleString()`   `valueOf()`

           返回函数代码

####  基本包装类型
***
 3个特殊的引用类型：Boolean,Number和String

每当读取一个基本类型值的时候，后台都会创建一个对应的基本包装类型的对象，以便我们能调用一些方法来操作数据，调用完后赋值null销毁该对象

引用类型与基本包装类型的主要区别：

使用new操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中，而自动创建的基本包装类型对象，则只存在与该行代码的执行瞬间，然后立即被销毁（所以我们不能为基本类型值添加属性和方法）。

- Boolean类型

   + 重写了`valueOf（）`方法，返回基本类型值true或false；重写了`toString（）`方法，返回字符串“true”和“false”
   +  注意点：
  
            var falseObject = new Boolean(false);
            var result = falseObject && true;
            alert(result)； // true，因为非空对象布尔值永远是true

- Number 类型

   - `toFixed()`方法

      接收一个参数，即要表示为几位小数（若原数小数位大于传入的参数，则采取四舍五入）

  - `toExponential()`

     接收一个参数，表示几位小数（但是转换为e表示法）

  - `toPrecison()`

     接收一个参数，表示数值的所有数字的位数（不包括指数部分）

- String 类型

   -  `charAt()`   `charCodeAt()`

        分别接受一个参数（基于0），其中`charAt()`以字符串方式返回指定位置的字符，而`charCodeAt()`返回字符编码
     
        另外可以使用方括号表示法访问字符串中的特定字符

  - 查找字符串方法

     + `indexOf()`
     + `lastIndexOf（）`
     
            搜索给定的子字符串，然后返回子字符串的位置（没有则返回-1）,只返回第一次出现的位置

            还有一个可选参数，指定从何处开始搜索
  - `trim（）` 

        创建一个字符串副本，删除前置和后缀的所有空格，然后返回结果

  - 大小写转换方法
      + `toLowerCase（）`
      + `toUpperCase（）`
      + `toLocaleLowerCase()`
      + `toLocaleUpperCase()`

        不清楚代码将在何种语言下运行的情况下，使用后两种方法较为稳妥

  - 字符串的模式匹配方法

     + `replace()`

            接收两个参数：第一个参数可以是RegExp对象或者一个字符串，第二个参数是一个字符串或者一个函数

            如果第一个参数是字符串，则只会替换第一个子字符串；要想替换所有子字符串，提供一个正则表达式并指定g（全局）标志

     + `split()`
     
            接收两个参数，分隔符和数组大小

     + `fromCharCode()`
     
            接收多个字符编码转换为一个字符串  

####  单体内置对象
***

- Global

   + URL编码方法

       + `encodeURL() ` `encodeURLComponent()`

            前者只会对不属于URL的特殊字符进行编码，例如冒号，斜杠，问号，井字号等均会保留；

            后者会对他发现的任何非标准字符进行编码

     + `decodeURL()`  `decodeURLComponent()`

   + `eval()`

        只接受一个参数，即要执行的ECMAScript字符串

- Math对象

    - `min()`  `max()`

        求数组中最小值和最大值

   - 舍入方法

     + `Math.ceil()`  数值向上舍入为整数
     + `Math.floor()` 向下舍入为整数
     + `Math.round()` 四舍五入

   - `random()`

        返回大于0而小于1的一个随机数

### 第六章 面向对象的程序设计
####  理解对象
***     
   - 属性类型

      - 数据属性

          - [[Configurable]]:能否通过delete删除属性从而重新定义属性，能否修改属性特性，或者能否把属性修改为访问器属性。默认为true
          - [[Enumerable]]: 能否通过for-in循环返回属性。默认为true
          - [[Writable]]:能否修改属性的值。默认为true
          - [[Value]]: 包含这个属性的数据值。读取和写入都是从这里开始。默认值为 undefined
          - 如何修改属性默认的特性？

             使用Object.defineProperty()方法，三个参数：属性所在的对象，属性的名字和描述符对象（以上四个之一）

                 Object.defineProperty(person,"name",{
                        writable:false,
                        value:"Tom"
                    });

          - 若把[[Configurable]]特性设置为false，则不能修改除writable之外的特性

      - 访问器属性

           - [[Configurable]]
          - [[Enumerable]]
          - [[Get]]:读取属性时调用的函数，默认为undefined
          - [[Set]]:在写入属性时调用的函数，默认为undefined

   - 定义多个属性

      使用`Object.defineProperties()`方法

   - 读取属性的特性

     使用`Object.getOwnPropertyDescriptor()`方法

     这个方法接收两个参数，属性所在的对象和要读取的属性名称。返回一个对象，其属性值包括上述四个描述符，访问即可。

 
####  创建对象
***    

- 工厂模式
  
         function createPerson(name,age,sex){
               var o = new Object();
               o.name = name;
               o.age = age;
               o.sex = sex;
               o.sayName = function (){
                     alert (this.name);
               };
              return o;
         }
         // 没有解决对象识别的问题（即如何判断该对象的类型）   
- 构造函数模式

         function Person(name,age,sex){
              this.name = name;
              this.age = age;
              this.sex = sex;
              this.sayName = function(){
                     alert(this.name);   
               };   
         }
         //构造函数可以用来创建特定类型或者自定义的对象，从而定义自定义对象类型的属性和方法；
         //构造函数函数名使用大写字母开头；
         //创建实例必须使用new操作符
         //person1既是Person的实例，也是Object的实例
          var person1 = new Person("Jack","24","male");
         //问题在于，每个实例上每个方法都要重创建一遍 ，若把方法置于全局，则封装性差

- 原型模式

       每个函数都有一个prototype属性，这个属性是一个指针，指向一个包含可以由特定类型的所有实例共享的属性和方法的对象。

       即prototype是通过构造函数创建的那个对象实例的原型对象。
         
         function Person(){
                   }
         Person.prototype.name = name;
         Person.prototype.age = age;
         Person.prototype.sex = sex;
         Person.prototype.sayName = function(){
                     alert(this.name);   
          };   
         

   - 理解原型对象

        创建新函数就会为该函数创建一个prototype属性，这个属性指向函数的原型对象，默认情况下，所有原型对象都会自动获得constructor属性，这个属性包含一个指向prototype属性所在函数的指针
  
        创建自定义构造函数后，原型对象默认只会获得constructor属性，其他方法均从Object继承而来；

        调用构造函数创建一个实例后，该实例内部包含一个指针（内部属性），指向构造函数的原型对象 ，ECMA5中叫做[[prototype]]

        无法访问到[[prototype]],但是可以调用`isPrototypeOf()`方法：

            alert (Person.prorotype.isPrototypeOf(person1));  // true

         ECMAScript5中增加的新方法  `Object.getPrototypeOf()`:
         
            alert(Object.getPrototypeOf(person1) == Person.prototype); // true

         每当代码读取某个对象的某个属性时，都会执行一次搜索，首先从对象实例本身开始，如果在实例属性中找到，则直接返回该属性的值；若没有找到，则继续搜索指针指向的原型对象

         当为对象实例添加一个属性时，这个属性会屏蔽掉原型对象中的同名属性，也就是说，不会修改原型对象中的同名属性值，只是阻止我们通过对象实例属性去访问它。

        使用`hasOwnProperty()`检测一个属性是存在于实例中，还是存在于原型中（只有在给定属性存在于对象实例中时返回true,存在于原型中或者压根儿不存在都是false）：

            alert(person1.hasOwnProperty("name"));

    - 原型与in操作符

        - 单独使用in操作符

                function hasPrototypeProperty（object，name）{
                          return  !object.hasOwnProperty(name) && name in object
                }
                //主要是要区分属性到底是不存在还是存在于原型中

        - for-in循环

             返回的是所有能够通过对象访问的，可枚举的属性（不论其存在于实例中还是原型中）

            屏蔽了原型中不可枚举属性的实例属性也会被枚举

       - `Object.keys() `

            接收一个对象作为参数返回一个包含所有可枚举属性的字符串数组

       - `Object.getOwnPropertyNames()`
       
            得到所有实例属性，不论其是否可枚举 

    - 更简单的原型语法

             function Person(){}
             Person.prototype = {
                   name:"王二"，
                   age：28，
                   sex：“male”，
                  sayName：function(){
                            alert(this.name);
                  }
            }

            var person1 = new Person();
            alert(person1 instanceof  Object);  // true
            alert(person1 instanceof Person);  // true
            alert(person1.constructor == Person); // false
            alert(person1.constructor == Object);  // true
            //这里的语法完全重写了默认的prototype对象
            //可以在属性中显式设置constructor属性值为Person，但是这样会导致它的[[Enumerable]]特性设置为true（即可以被枚举）。

    - 原型的动态性

         原型中查找值是一次搜索，所以对原型对象做的任何修改都可以立即从实例中反映出来；

         重写原型对象切断了现有原型和实例之间的联系。

    - 原型对象的原型

         通过原声对象的原型，不仅可以取得所有默认方法的引用，而且也可以定义新方法。

    - 原型对象的问题

         - 默认情况下所有实例都取得相同的属性值；
         - 不管是基本类型值还是引用类型值，都可以通过在实例上添加一个同名属性来隐藏原型中的对应属性（书上说基本类型值和引用类型值不同，只是说向其中数组添加新字符串时候会影响全局）

- 组合使用构造函数模式和原型模式    

    构造函数模式用于定义实例属性，原型模式用于定义方法和共享的属性

        function Person(name,age,sex){
               this.name = name;
               this.age = age;
               this.sex = sex;
        }
        Person.prorotype = {
              constructor :Person,
              sayName: function(){
                 alert(this.name); 
              }
        }
        //此时若创建新实例，实例数组作修改不会影响另一个实例
        //此方法是目前使用最广泛，认同度最高的一种创建自定义类型的方法

- 动态原型模式

      通过检查某个方法是否存在来初始化原型

        function Person(name,age,sex){
              this.name = name;
              this.age = age;
              this.sex = sex;
              if(typeof this.sayName != "function"){
                   Person.prototype.sayName = function(){
                      alert(this.name);
                       }
                   }
         }
        //如果有很多要进行初始化的属性和方法，只需要检查其中一个即可
        //很完美

- 寄生构造函数模式

     与工厂模式差不多，只是使用了new操作符创建实例

    构造函数在不返回值的情况下，默认会返回新对象实例；而通过在构造函数末尾添加return语句，可以重写调用构造函数时返回的值

    这种模式下差ungjiande实例与构造函数以及构造函数的原型之间没有关系

    不建议使用。

- 稳妥构造函数模式

     稳妥对象指的是没有公共属性，且其方法不引用this的对象。

     大体与寄生构造函数模式一样，不同点为：一是实例方法不使用this；二是不使用new操作符调用构造函数

    适合于某些安全执行环境

####  继承
***    

许多OO语言都支持两种继承方式：接口继承和实现继承；

接口继承只继承方法签名，实现继承则继承实际的方法。

ECMAScript中的函数没有签名，所以只支持实现继承，而实现继承主要依靠原型链来实现。

- 原型链

    - 本质就是将A函数的实例赋给B函数的原型对象，这样B函数的原型对象中就拥有了A函数原型对象的方法，B函数的实例同样如此，即实现了继承。

    - 所有函数的默认原型都是Object的实例，因此默认原型均包含一个指向Object.prototype的指针；

    - 如何确定原型和实例之间的关系？

        - 使用 instanceof操作符    （实例与原型链中出现过的构造函数）
        - 使用 isPrototypeOf() 方法   （实例与原型链所派生的实例的原型）

- 借用构造函数

        function SuperType(){
          this.colors = ["red","blue","green"];
        }
        SuperType.prototype.sayColors = function() {
          alert(this.colors);
        }
        function SubType(){
         //继承了SuperType，
         //实际上是(未来将要)新建的SubType实例的环境下调用了SuperType构造函数，这样SubType的每个实例都会具有自己的colors属性的副本了，这样在各个实例中修改colors数组不会相互影响了
         //sayColors却无法继承
         SuperType.call(this);
        }
- 组合继承

    综合原型链和构造函数两者之长

        function SuperType(name){
          this.name = name;
          this.colors = ["red","blue","green"];
        }
        SuperType.prototype.sayColors = function() {
          alert(this.colors);
        }
        function SubType(name，age){
         //继承了SuperType的属性
         SuperType.call(this，name);
         this.age = age;
        }
         //继承方法
         SubType.prototype = new SuperType();
         SubType.prototype.constructor = SubType;
         SubType.prototype.sayAge = function() {
                   alert (this.age);
         };

- 原型式继承

        var person = {
                  name: "Tom";
                  friends:["Jack","Sawyer","John"];
        }
        var aontherPerson = Object.create(person);
        anotherPerson.friends.push("Bob");
        alert(person.friends);   //"Jack","Sawyer","John","Bob"

- 寄生式继承

        function createAnother(original){
            var clone = object(original);
            clone.sayHi = function(){
               alert("hi");
               };
            return clone;
        };

- 寄生组合式继承

    解决两次调用问题   

     [构造函数的继承](http://www.jb51.net/article/28128.htm)

     [非构造函数的继承](http://www.jb51.net/article/28129.htm)

     //以上两个链接讲的很清楚，赞

### 第七章 函数表达式

定义函数的方式：函数声明；函数表达式

#### 递归  
***     

arguments.callee是一个指向正在执行的函数的指针、

#### 闭包  
***     
作用域链实质上是一个指向变量对象的指针列表，它只引用但并不包含变量对象；

一般来说，函数执行完毕后，局部活动对象就会被销毁，内存中仅保存全局作用域。

闭包中可以将内部函数设置为null，以便释放内存

- 闭包与变量

        function createFunctions(){
            var result = new Array();
            for (var i = 0; i<10;i++){
                result[i] = function(){
                       return i;  
                      }
                }
           return result;
        }
        // 执行该函数返回的数组全是10
        // 因为闭包保存的是整个变量对象，而不是某个变量的值（在这里保存了i的引用）

- 关于this对象
  
    这块儿多看文章吧
   
- 内存泄漏

    在IE旧版本中，若闭包的作用域链中保存着一个HTML元素，那么意味着该元素将无法被销毁（循环引用）

#### 模仿块级作用域 
***     

  JavaScript从来不会告诉你是否多次声明了同一个变量：遇到这种情况只会对后续的声明视而不见（但是会执行后续声明中的变量初始化）

  - 如何创建私有作用域？
   
            (function(){
               //这里是块级作用域
               }) () 

        临时需要一些变量的时候可以使用私有作用域

#### 私有变量 
***   

   在对象上创建特权方法的方式：

   - 在构造函数中定义特权方法

            function MyObject(){
                  //私有变量和私有函数
                  var privateVariable = 10;
                  function privateFunction(){
                     return false;  
                  }
                 //特权方法
                 this.publicMethod = function(){
                    privateVariable++;
                    return privateFunction();
                 }
            }
   - 静态私有变量
   - 模块模式
   - 增强的模块模式

### 第八章 BOM

#### window对象 
***  
BOM核心对象是window，它表示浏览器的一个实例。在浏览器中，window对象既是通过JavaScript访问浏览器窗口的一个窗口，又是ECMAScript规定的Global对象。

- 全局作用域
      
    所有在全局作用域中声明的变量，函数都会变成window对象的属性和方法。

    全局变量不能通过delete操作符删除，而直接在window对象上定义的属性可以删除。

    尝试访问未声明的变量会抛出错误，但是可以通过查询window对象知晓某个可能未声明的变量是否存在

         var  newValue = oldValue;   // 抛出错误，因为oldValue未定义；

         var newValue = window.oldValue;  //不会抛出错误，只是一次属性查询；

- 窗口关系及框架

    与window对象相关的几个属性：top parent self

     - top 

        top对象始终指向最高（最外）层的框架，也就是浏览器窗口
     - parent
     
        始终指向当前框架的直接上层框架

        在某些情况下，parent有可能等于top；但在没有框架的情况下，parent一定等于top（都等于window）  

    - self
    
        始终指向window	  

- 窗口位置

      IE,Safari,Opera和Chrome提供` screenLeft `和`screenTop`属性，分别用于表示窗口相对于屏幕左边和上边的位置；

      Firefox则在`screenX`和`screenY`属性中提供相同的窗口位置信息（safari和chrome同时支持这两个属性）

    不同点： IE，Opera中保存的是可视窗口到屏幕的距离（即不包括浏览器工具栏宽度），而其余浏览器中保存的是整个浏览器窗口到屏幕边的距离

    `moveTo()` 接收新位置的x和y的值； `moveBy()`接收在水平或者垂直方向移动的像素数


### 第九章 客户端检测

### 第十章 DOM

DOM是针对HTML和XML文档的一个API（应用程序编程接口）

#### 节点层次 
***       

文档节点是每个文档的根节点

文档元素是文档的最外层元素，文档中的其他所有元素都包含在文档元素中。每个文档只能有一个文档元素。

在HTML页面中，文档元素始终都是<html>元素。在XML中，没有预定义的元素，因此任何元素都可能成为文档元素。

- Node类型

    DOM1级定义了一个Node接口，该接口将由DOM中的所有节点类型实现。
    
    JS中的所有节点类型都继承自Node类型，因此所有节点类型都共享这相同的基本属性和方法。

    每个节点都有一个nodeType属性，用于表明节点的类型。节点类型由在Node类型中定义的下列12个**数值常量**来表示：

    Node.ELEMENT_NODE(1);

    Node.ATTRIBUTE_NODE(2);

    Node.TEXT_NODE(3);

    Node.CDATA_SECTION_NODE(4);

    ....

        //由于IE没有公开Node类型的构造函数，下列判断节点类型方法在IE中无效：
        if（someNode.nodeType == Node.ELEMENT_NODE）{
           alert("Node is an element")；
        }
        //保证兼容，采用下列方法
        if(someNode.nodeType == 1){
           alert("Node is an element");
        }

     - nodeName和nadeValue属性

         对于元素节点，nodeName中保存的始终是元素的标签名，而nodeValue的值始终是null。

     - 节点关系

         - 每个节点都有一个childNodes属性，其中保存着一个NodeList对象。NodeList是一种类数组对象，用于保存一组有序的节点，可以通过位置来访问这些节点（可以通过方括号语法访问NodeList的值，而且也有length属性，但是它不是Array的实例）。

        -   NodeList对象独特之处：实际上是基于DOM结构动态执行查询的结果，因此DOM   结构能够自动反映到NodeList对象中。

                someNode.childNodes[0];
                someNode.childNodes.item[0];
                someNode.childNodes.length;  //访问的都是那一个瞬间的状态！

       - 如何将NodeList对象转换为数组？

                function convertToArray(nodes){
                     var array = null;
                     try  {
                         array = Array.prototype.slice.call(nodes,0); 
                        //针对非IE浏览器,0是传给slice方法的，表示从头开始遍历
                       }catch(ex){
                         array = new Array();
                         for (var i = 0,len = nodes.length; i<len; i++){
                                array.push(nodes[i]);
                               }
                    }
                   return array;
                }
                //nodes指的是someNode.childNodes

         
        - 每个节点都有一个parentNode属性，该属性指向文档树中的父节点。此外，在childNodes列表中的每个节点之间都是同胞节点previousSibliing和nextSibling

        - `hasChildNodes()`在节点包含一或多个子节点的情况下返回true
        - 所有节点都有的一个属性ownerDocument，该属性指向表示整个文档的文档节点

     - 操作节点

        关系指针全部是只读的。

        以下方法都是在父节点上进行操作：

        - `appendChild()`

            用于向childNodes列表的末尾添加一个节点；若该节点已经存在于DOM中，则将其移动到末尾位置（任何DOM节点不能同时存在于文档中的多个位置上）

        - `insertBefore()`

            接收两个参数：要插入的节点和作为参照的节点。

            插入节点后，被插入的节点会成为作为参照的节点的前一个同胞节点，同时被返回；若参照节点是null，则执行与`appendChild()`相同的操作。

        - `replaceChild()`

            接收两个参数：要插入的节点和要替换的节点，返回要替换的节点

        - `removeChild()`

            接收一个参数：即要移除的节点

     - 其他方法

        - `cloneNode()`

            用于创建调用这个方法的节点的一个完全相同的副本（不会复制添加到DOM节点中的js属性）

            接收一个布尔值参数，true执行深复制，也就是复制节点及其整个子节点树；false即只复制节点本身。

            复制后返回的节点副本属于文档所有，但并没有为它指定父节点。 成为了“孤儿”。
        - `normalize()` 

            处理文档树中的文本节点。当在某个节点上调用这个方法时，找到空文本则删除它；如果找到相邻的文本节点，则将它们合并为一个文本节点。

- Document类型

       document对象是HTMLDocument的一个实例，表示整个HTML页面。

      document对象是window对象的一个属性，因此可以作为全局对象来访问。

       - 文档的子节点
   
          内置的访问子节点的快捷方式：

           -  documentElement属性
           -  通过childNodes列表访问文档元素
          - `document.body`直接指向body元素 
          - 可能的子节点 DocumentType，通过document.doctype属性访问信息

          文档类型是只读的，而且它只能有一个元素子节点.

      - 文档信息

           - `title`

              `document.title`取得当前页面的标题，也可以修改（会改变`<title>`元素）

           - `URL` ， `domain` 和`referrer`

               `URL`中包含页面完整的URL（即地址栏显示的URL）；

               `domain`只包含页面的域名；

              `referrer`中保存着链接到当前页面的那个页面的URL（无则包含空字符串）

               三个属性中只有domain可以设置，但是不能将这个属性设置为URL中不包含的域。另外如果将其设置为wrox.com之后就不能再将其设置回p2p.wrox.com了。（即不能从松散loose回到紧绷tight）

       - 查找元素

           - `getElementById()`

              IE8及较低版本不区分ID大小写

          - `getElementsByTagName()`

              在HTML文档中返回一个HTMLCollection对象，与NodeList非常类似，即可以像数组那样用方括号语法或item()方法访问其中的项。

             HTMLCollection对象有一个namedItem()方法，可以取得元素集中name属性为特定值的元素；同时支持用name属性值方括号访问元素

          - `getElementsByName()`

             返回带有给定name特性的所有元素

       - 特殊集合
       - DOM一致性检测
                  
           document.implemention.hasFeature()接收两个参数：要检测的DOM功能名称和版本号

       - 文档写入

          - `write()`和`writeIn()`

             write()会原样写入，writeIn()则会在字符串末尾添加一个换行符（\n）

             文档加载结束后再调用document.write()那么输出的内容将会重写整个页面

          - `open()`和`close()`

             用于打开和关闭网页输出流

- Element类型

     要访问元素的标签名，可以使用`nodeName`，也可以使用`tagName`。

      - HTML元素 

           所有HTML元素都由HTMLElement类型表示
     - 取得特性

           - `getAttribute()`

               甚至可以取得自定义特性，根据HTML5规范，自定义特性应该加上data-前缀以便验证

               通过该方法访问style属性时，返回css文本，而通过.属性访问则返回一个对象（style属性是以变成方式访问元素样式的）；

               通过该方法访问onclick时，返回相应代码的字符串；通过属性访问时则返回一个js函数

      - 设置特性
           - `setAttribute()`

              可以操作HTML特性，也可以操作自定义特性。通过该方法设置的特性名会被统一转换为小写。
           - `removeAttribute()`

               不仅会删除特性的值，而且会从元素中完全删除特性

      - attributes属性

         Element类型是使用attributes属性的唯一一个DOM节点类型。

         attributes属性中包含一个类似于NodeList的NamedNodeMap         
     - 创建元素

         - `document.createElement()`

            只接受一个参数，即要添加的元素的标签名
    - 元素的子节点

        IE解析会包括文本节点，其余浏览器会忽略掉文本节点

- Text类型

     每个可以包含内容的元素最多只能有一个文本节点（必须有确实内容存在，空格也可）

     修改文本时，字符串会经过HTML编码（被转义）
         
   - 创建文本节点
 
        `document.createTextNode()`  

         只接受一个参数，要插入节点中的文本

        若两个文本节点是相邻的同胞节点，那么这两个节点中的文本就会连起来显示，中间不会有空格


   - 规范化文本节点

        `normalize()`

         若在一个包含两个或者多个文本节点的父元素上调用该方法，则会将所有文本节点合并成一个节点，结果节点的nodeValue值等于合并前每个文本节点的nodeValue值拼接起来的值。

  - 分割文本节点

        `splitText()`

         接收一个参数，从该参数指定位置进行分割

        这是从文本节点中提取数据的常用DOM解析技术

- Comment类型

    与Text类型继承自相同的基类，所以拥有除splitText()之外的所有字符串操作方法。

- CDATASection类型
- DucumentType类型

    document.doxtype.name  保存着文档类型

- DocumentFragment类型

    文档片段，用于避免多次添加内容到文档树上导致的重复渲染。

    即先添加到文档片段上，在一次性添加到文档树上（文档片段本身永远不会成为文档树的一部分）

- Attr类型

    元素的特性类型，一般不使用

#### DOM操作技术
***     

- 动态脚本

    指的是页面加载时候不存在，但在将来某一时刻的时候通过修改DOM动态添加的脚本。

    IE将`<script>`视为一个特殊的元素，不允许DOM访问其子节点。但是可以使用`<script>`元素的text属性来指定js代码

- 动态样式

    指的是～～～的样式

    IE存在与上述相同的问题，可以访问styleSheet属性的cssText属性来修改。

    将cssText设置为空字符串可能会导致IE崩溃。

- 操作表格
- 使用NodeList

    理解 NodeList   NamedNodeMap   HTMLCollection 三个动态对象

### 第十一章 DOM扩展

#### 选择符API
***     

- `querySelector()`
 
    接收一个css选择符，返回与其匹配的第一个元素（可以在Document类型上调用，也可在Element类型上调用）

- `querySelectorAll()`

    接收一个css选择符，但是返回所有匹配的元素（NodeList的实例），底层实现类似于一组元素的快照，而非不断对文档进行搜索的动态查询

- `matchesSelector()`

    接收一个css选择符。若调用元素与选择符想匹配返回true；否则返回false 。

    该方法只能用于Element类型，而上述两个方法Document类型，DocumentFragment类型和Element类型均可使用

#### 元素遍历
***
对于元素间的空格，IE9及之前版本不会返回文本节点，而其他浏览器则会返回文本节点。这样使用childNodes和firstChild等属性时候行为将不一致。所以新定义了一组属性来弥补这一差异。

#### HTML5
***

   - 与类相关的补充

       - `getElementsByClassName()`

           接收一个参数，返回带有指定类的所有元素的NodeList。
       - classList属性

           修改操作className的方法。这个classList是新集合类型DOMTokenList的实例。

           还定义如下的方法：

           `add(value)`：将给定的字符串添加到列表中。若值已经存在，则忽略；
  
           `contains(value)`:表示列表中是否有给定的值，存在则返回true；

           `remove(value)`:从列表中删除给定的字符串；

           `toggle(value)`：若列表中存在给定的值，删除它；若没有，添加它。

  - 焦点管理

     `document.activeElement()`始终引用DOM中当前获得了焦点的元素；

      默认情况下，文档刚刚加载完成时，此属性中保存的是document.body元素的引用。文档加载期间，该属性的值为null。

      元素获得焦点的方法：页面加载，用户输入(Tab键)和调用focus()方法。

      `document.hasFocus()`用来检测文档是否获得了焦点，可以确定用户是不是正在与页面交互

  - HTMLDocument的变化 

       - `document.readyState`

           有两个可能的值，loading(正在加载文档)；complete(已经加载完文档)  。

       - `document.compatMode`

           标准模式下值为CSS1Compat；混杂模式下值为BackCompat
       - `document.head`

           引用文档的head元素

  - 字符集属性

       - `document.charset`

           可以通过<meta>元素，http响应头部或者设置charset属性修改文档中实际使用的字符集

      - `document.defaultCharset`

           表示默认字符集是什么

   - 自定义数据属性

       HTML5规定可以为元素添加非标准的属性，但要添加前缀data-，提供与渲染无关的信息或者语义信息

       添加了自定义属性之后可以通过元素的dataset属性来访问自定义属性的值。dataset属性的值是DOMStringMap 的一个实例，也就是一个名值对儿的实例。在这个映射中，属性名没有data-前缀。

   - 插入标记

       - innerHTML属性

           - 读模式下，innerHTML属性会返回与调用元素的所有子节点（包括元素注释和文本）对应的HTML标记；
           - 写模式下，innerHTML属性会根据指定的值创建新的DOM树，然后用这个DOM树完全替换调用元素原先的所有子节点。

      - outerHTML属性

           - 读模式下，返回调用它的元素及所有子节点的HTML标签；
           - 写模式下，根据指定的HTML字符串创建新的DOM子树，然后用该子树完全替换调用元素 

      - `insertAdjacentHTML()`

        接收两个参数，第一个是指定插入位置，第二个是要插入的HTML文本

       - 内存与性能问题
        
         使用前述方法时，最好先手工删除要被替换的元素的所有事件处理程序和js对象属性。（元素删除之后，其与绑定的事件关系并未删除）

   - `scrollIntoView() `
          
       可以在任何元素上调用，通过滚动浏览器窗口或某个窗口元素，调用元素就可以出现在视口中。

       - 传入true或者不传参，那么窗口滚动之后会让调用元素的顶部与视口顶部尽可能平齐
       - 传入false，顶部不一定平齐

#### 专有扩展
***

- 文档模式
- children属性

    HTMLCollection的实例，只包含元素中同样还是元素的子节点

- `contains()`
 
    由父元素调用，接收一个参数，即要检测的后代节点。（检测某个节点是不是父节点的后代节点）

- 插入文本

  -  innerText属性
  -  outerText属性

### 第十三章 事件

#### 事件流
***     

事件流指的是从页面中接收事件的顺序。

-  事件冒泡

    IE的事件流叫做事件冒泡(event bubbling)，即事件开始时由最具体的元素接收，然后主机向上传播到较为不具体的节点（文档）

- 事件捕获

    事件捕获的思想是不太具体的节点应该更早接收到事件，而最具体的节点应该最后接收到事件。

    事件捕获的用意在于事件到达预定目标之前捕获它。

- DOM事件流

    DOM2级事件规定的事件流包括三个阶段：事件捕获阶段，处于目标阶段以及事件冒泡阶段。

    DOM2级事件规范明确要求捕获阶段不会涉及事件目标，但是浏览器都会在捕获阶段触发事件对象上的事件，结果就是有两个机会在目标对象上操作事件。
#### 事件处理程序
***     

事件就是用户或浏览器自身执行的某种动作，诸如click，load，mouseover等；

事件处理程序（事件侦听器）就是响应某个时间的函数，名字以"on"开头，诸如 onclick，onload等。

- HTML事件处理程序 

    缺点：

     1 存在时差问题，在定义函数之前发生事件则会引发错误；

     2  扩展事件处理程序的作用域链在不同浏览器中会导致不同结果；

     3 HTML与JS代码紧密耦合，不利于复用。

- DOM0级事件处理程序

     直接将一个函数赋值给一个事件处理程序属性。
- DOM2级事件处理程序

    `addEventListener()` 和`removeEventListener()`

     接收三个参数，要处理的事件名，作为事件处理程序的函数和一个布尔值（true时在捕获阶段调用事件处理程序，false时在冒泡阶段调用事件处理程序）

     通过`addEventListener()` 添加的事件处理程序只能通过`removeEventListener()`来移除，移除时传入的参数与添加处理程序时使用的参数相同（如果是匿名函数，则将无法移除）

    多数情况下，都是将事件处理程序添加到事件流的冒泡阶段，这昂可以最大限度地兼容各种浏览器。最好只在需要在事件到达目标之前截获它的时候将事件处理程序添加到捕获阶段

- IE事件处理程序

    `attachEvent()`和`detachEvent()`

      接收两个参数：事件处理程序名称（带有on前缀的，区别于DOM2级事件处理程序）与事件处理程序函数。

      在使用DOM0级方法的情况下，this指向事件所属元素；在attachEvent()方法下，this指向window。

      用该方法为某个元素添加两个不同的事件处理程序，将以添加的顺序相反顺序执行（区别于DOM2）

- 跨浏览器的事件处理程序

 #### 事件对象
***     


