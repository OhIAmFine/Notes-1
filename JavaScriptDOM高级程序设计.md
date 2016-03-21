##Part 1 深入理解DOM脚本编程

### 第一章  遵循最佳时间

#### 不唐突和渐进增强
***

XHTML用于提供文档结构的语义标记，CSS为文档布局提供定位和样式，DOM脚本编程用于增强文档的行为和交互性。

渐进增强（progressive enhancement）和优雅降级（graceful degradation）

编写的脚本遵循以下原则：

   - 与标准兼容
   - 容易维护
   - 可访问
   - 可重用

####让JavaScript运行起来
***

 - 把行为从结构中分离出来

       - 如何以正确的方式包含JavaScript？


           嵌入式脚本与其他标记混合添加；           **不推荐**

           添加到头部元素中；                                **不推荐**

           通过外部源文件来包含JavaScript脚本。   **最好的做法**

       - 昔日的javascript：前缀

          最佳方案：在window载入时添加事件处理程序

- 不要版本检测

    版本检测或浏览器嗅探是错误的做法（考虑适应未来future-proofing！！）

    - 使用能力检测

        执行代码之前检测某个脚本对象或者方法是否存在，而不是依赖于你对哪个浏览器具有哪些特性的了解。

    - 何时使用浏览器版本嗅探

         若每一个浏览器都实现了同一个对象，但与这个对象及其方法或属性的交互方式不同，也不可能根据一个特殊对象或方法的存在来修改脚本代码。此时就应当使用版本嗅探。

- 通过平稳退化保证可访问性
- 为重用命名空间而进行规划

    使用包围函数（自执行的匿名函数）

        (function(){
              //code
        })()
- 通过可重用的对象把事情简化

    - 开始构建库（命名为STS）

            if(!window.STS){window['STS'] = {}}
            //以便能在多个文件中使用相同的命名空间

    - `STS.isCompatible()`
s
         用于确定当前浏览器是否与整个库兼容。

            function  isCompatible(other){
                  //使用能力检测来检查必要条件
                 if（other === false || !Array.prototype.push || !Object.hasOwnProperty
                      || !document.createElement || !document.getElementByTagName ）
                     {return false};
                 return true;
             }
            window['STS']['isCompatible'] = isCompatible;


             if(STS.isCompatible()) {
                      //使用库中代码
              }   

  - `STS.$()`

            function $(){
                var elements = new Array();

                    //查找提供的每个参数
               for(var i = 0; i<arguments.length;i++){
                  var element = arguments[i];
                
                    //若该参数是一个字符串，则假设它是一个id名
                    if(typeOf element == ‘string’){
                       element = document.getElementById(element);
                    }
                    if (argument.length == 1){
                       return element;
                    }
                    elements.push(element); 
               }
              
                // 返回多个元素的数组
                return elements;
            };
             window['STS']['$'] = $;

   - `STS.addEvent()`和 `STS.removeEvent()`