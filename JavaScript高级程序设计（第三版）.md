
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

         建议做法：放在`</body>`前或包裹于`window.onload=function(){}`中

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
 			alert("yes");  //  "yes"
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

         可以用于任何数据类型（null值返回0，undefined值返回NaN，对象的话先调用`valueOf（）`，若返回NaN，则调用`toString()`）

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

  + `map（）`

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

   - 继承的toString()   toLocaleString()   valueOf()

           返回函数代码
 

     