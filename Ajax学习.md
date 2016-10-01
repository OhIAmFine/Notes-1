##什么是AJAX

- 全称： Asyncchronous JavaScript and XML（异步的JavaScript和XML）
- 不是编程语言
- 是一种无需重新加载整个网页的情况下能更新部分网页的技术（使用了ajax技术的网页通过在后台跟服务器进行少量的数据交换实现异步局部更新）
- 如何实现？
 + 运用HTML和CSS来实现页面，表达信息；
 + 运用XMLHttpRequest和web服务器进行数据的异步交换；
 + 运用JavaScript操作DOM，实现动态局部刷新

- HTTP相关

  + HTTP请求过程：
  
        1.建立TCP连接

        2.Web浏览器向Web服务器发送请求命令

        3.Web浏览器发送请求头信息

        4.Web服务器应答

        5.Web服务器发送应答头信息

        6.Web服务器向浏览器发送数据

        7.Web服务器关闭TCP连接

  + 请求的组成

         1.HTTP请求的方法或者动作，比如是GET（默认）还是POST请求

           +  GET： 一般用于信息获取；使用URL传递参数（对于任何人均可见）；对所发送信息的数量有所限制，一般2000个
           
           +  POST：一般用于修改服务器上的资源；对所发送的信息数量无限制     

         2.正在请求的URL

         3.请求头，包含一些客户端环境信息，身份验证信息等

         4.请求体，即请求正文

  + 响应的组成

         1.一个由数字和文字组成的状态码，用来显示请求成功还是失败

           + 1XX：信息类，表示收到Web浏览器请求，正在进一步处理中
           + 2XX：成功，表示用户请求被正确接收，理解和处理  如：200 OK
           + 3XX：重定向，表示请求没有成功，客户必须采取进一步动作
           + 4XX：客户端错误，表示客户端提交请求有错误
           + 5XX：服务器错误，表示服务器不能完成对请求的处理

         2.响应头，服务器类型，日期时间，内容类型和长度等

         3.响应体，即响应正文
- PHP
   + 一种创建动态交互性站点的服务器端脚本语言
- JSON
  + JavaScript对象表示法（JavaScript Object Notation）
  + JSON是存储和交换文本信息的语法，类似XML。采用键值对的方式来组织，易于人们阅读和编写，同时也易于机器解析和生成
  + JSON是独立于语言的，即不论什么语言都可以解析JSON，只需要按照JSON的规则来就行
  + JSON与XML比较
      + json长度比xml格式短小
      + json读写速度更快
      + json可以使用JavaScript内建的方法直接进行解析转换为JavaScript对象，很方便
  + JSON语法规则
      + JSON数据书写格式：名称/值对（名称和值对均用双引号括住，中间用冒号隔开）
      + JSON的值类型：数字  字符串 布尔值 数组（方括号） 对象（花括号） null
  + JSON解析
      + eval和JSON.parse
      
      		     eval（ ‘（’ +jsondata+  ‘）’ ）；
                 JSON.parse(jsondata);
      + 尽量不用eval解析，因为当json中含有恶意js代码时候，eval会直接执行代码，而JSON.parse则会抛出错误 
  + JSON校验工具
  
          jsonlint.com
       
        

- 创建XMLHttpRequest对象

        var request；

         if(window.XMLHttpRequest){

         request=new XMLHttpRequest();  // IE7+,Firefox,Chrome,Opera,Safari

         }else{

         request=new ActiveXObject("Microsoft.XMLHTTP"); // IE6,IE5

         }


  + open（method，url，async）
 
         method  请求方式GET还是POST   url 请求地址

  + send （string）
  
        我们使用get请求时，因为get 请求是没有主体的，所有参数都拼在url中，所以使用send 时这个参数可以不填写，也可以填写none;如果使用post 请求，这个send 一定要填写参数

  + readyState属性

        + 0：请求未初始化，open还没有调用
        + 1：服务器连接已经建立，open已经调用
        + 2：请求已接收，也就是接收到头信息了
        + 3：请求处理中，也就是接收到响应主体了
        + 4：请求已完成，且响应已就绪，即响应完成了

                var request = new XMLHttpRequest();

                request.open("GET","get.php",true);

                request.send();

                request.onreadystatechange = function(){

                 if(request.readyState===4&&request.status===200){

                   //do something  request.responseText                                
                   }
                  }
         
   + `request.setRequestHeader("Content-Type","application/x-www-form-urlencoded");`

        当请求方式为POST时，一定要设置如上的代码

- 用JQuery实现Ajax      

    jQuery.ajax([settings])
  + type: 类型，”POST“或”GET“，默认为”GET“
  + url：发送请求的地址
  + data：是一个对象，连同请求发送到服务器的数据
  + dataType：预期服务器返回的数据类型。若不指定，jQuery将自动根据HTTP包MIME信息来只能判断，一般我们采用json格式，可以设置为”json“
  + success：是一个方法，请求成功后的回调函数。
  + error：是一个方法，请求失败时调用此函数。传入XMLHttpRequest对象

- 跨域

  + 一个域名地址的组成：

         http://      www.      abc.com    :   8080    /   scripts/jquery.js

         协议     子域名      主域名        端口号           请求资源地址

         当协议，子域名，主域名，端口号中任意一个不相同时，都算作不同域

         不同域之间相互请求资源，就算做”跨域“

  + JavaScript出于安全方面的考虑，不允许跨域调用其他页面的对象
  + 处理跨域方法
      + 代理
      
             通过在同域名的web域名服务器端创建一个代理（后台调用异域服务，再把响应结果返回给前端，这样就相当于跨域了）

      + JSONP

                // 在www.aaa.com页面中：

                <script>
                function jsonp(json){
                        alert(json["name"]);
                }
                </script>
                <script  src="http://www.bbb.com/jsonp.js"></script>

                 //在www.bbb.com页面中：

                 jsonp({‘name’：'洪七'，‘age’：‘24’})；

            **不支持POST请求**

      + XHR2

               HTML5提供的XMLHttpRequest Level2已经实现了跨域访问以及其他的新功能

               IE10以下版本均不支持

               只需在后端做一些小改动：

                header(‘Access-Control-Allow-Origin:*’);
                header(‘Access-Control-Allow-Methods:POST,GET’);

      