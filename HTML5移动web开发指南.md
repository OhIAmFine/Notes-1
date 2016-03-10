### 第一章 移动互联网时代的Web技术

- 智能手机的移动Web浏览器特点

  - 有限的屏幕尺寸
  - 触屏，缩放
  - 硬件设备的提升
  - 基于Webkit内核

### 第二章 移动设备HTML5页面布局

#### 页面语义化简介
***
- HTML5新语义元素概述

   - `<header>`

        定义文档的页面组合，通常是一些引导和导航信息

   - `<footer>`

        定义文档或章节的末尾部分，通常包含一些章节的基本信息，如作者信息，版权信息等

        一个HTML页面上可以允许有一个或多个header和footer

   - `<nav>`

        用来构建导航，显示导航链接

   - `<aside>`

        定义边栏，显示非正文内容 

   - `<article>`

        表示文档，页面，用来显示一块独立的文章内容。可以相互嵌套
 
   - `<section>`

        定义为文档中的节，比如章节，页眉，页脚或其他部分

   - `<hgroup>`

        对网页或区段的标题元素进行组合

- 页面结构与移动设备的布局

### 第三章 HTML5规范的本地存储

HTML5本地存储规范中定义了两个API：Web Storage和本地数据库Web SQL Database

Web Storage实际上是HTML4中Cookies存储机制的一个改进版本，其作用是在网站中把有用的信息存储到本地的计算机或移动设备上，然后根据实际需要从本地读取信息

Web Storage提供了两种存储类型API接口：sessionStorage和localStorage;sessionStorage生命周期仅在会话期间有效，而localStorage存储在本地，永久存储，除非用户删除。


#### 移动设备的支持
***        

    if(window.localStrorage){
    //浏览器支持localStorage
    }

    if(window.sessionStorage){
    //浏览器支持sessionStorage
    }

#### localStorage
***    

- 安全性方面

   基于域，然和该域内的页面都可以访问localStorage数据；

   存在问题，各个浏览器之间数据是相互独立的，不能跨域访问。

- API

    - 如何存储一个数据?
   
            localStorage.setItem("name","John");
            //以key/ value 形式存储
    - 如何读取一个数据？

            localStorage.getItem("name");

            localStorage.key(1);   //该方法效果同上，但要确定存储列表中只有一个item

    - 如何删除数据？

            localStorage.removeItem("name");  //删除指定key为“name”的键值对item

            localStorage.clear();//删除所有键值对

   - 如何存储和读取JSON格式数据？

            var userData = {
                  name = "wang wu";
                  sex = "male";
                  age = "55"
             };

            // 存储userData数据
            localStorage.setItem("userData",JSON.stringify(userData));
            // 读取userData数据并且赋值给新变量
            var newUserData = JSON.parse(localStorage.getItem("userData"));
            //删除本地item
            localStorage.remove("userData");

#### sessionStorage
***    

   API用法与localStorage相似

#### Storage事件监听
*** 

Storage事件可以使用W3C标准的注册事件方法addEventListener进行注册监听

    window.addEventListener("storage",showStorageEvent,true);

### 第四章 移动Web的离线应用

网页缓存与离线应用的区别：

  - 网页缓存依赖于网络存在，而离线应用在离线状态下仍然可以使用
  - 网页缓存主要缓存当前页面相关内容，也仅限于当前页面的读取；离线应用则主要缓存文件，只要设置缓存该文件的页面，都能在离线状态下读取该文件

#### 移动设备的支持
*** 

    if(window.applicationCache){
        // 浏览器支持离线应用
    }