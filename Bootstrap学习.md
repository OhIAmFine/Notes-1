- Bootstrap是什么？

    简单，灵活的用于搭建Web页面的HTML，CSS，JavaScript的工具集

- Bootstrap模板


        <!DOCTYPE html>
        <html lang="en">
        <head>
        <meta charset="utf-8">

        <!-- 由于Bootstrap不支持IE兼容模式，下列这行代码是让IE运行最新的渲染模式 -->
        <meta http-equiv="X-UA-Compatible" content="IE=edge">

        <!-- 初始化移动浏览显示：视口宽度等于设备物理宽度，初始缩放比例为1 -->
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <!-- 以上三个标签必须置于head标签中最前，其余元素置于其后 -->

        <title>Bootstrap 101 Template</title>

        <!-- 载入Bootstrap的CSS文件 -->
        <link href="css/bootstrap.min.css" rel="stylesheet">

        <!-- Bootstrap不支持IE7及低版本，以下第一个js文件是为了让IE8及低版本支持HTML5标签，第二个是使其支持媒体查询(media queries) -->
        <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
        <!--[if lt IE 9]>
        <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
        <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
        <![endif]-->
        </head>
        <body>
        <h1>Hello, world!</h1>

        <!-- Bootstrap中的JS插件依赖于jQuery，因此jQuery要在Bootstrap之前引用 -->
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
        <!-- 载入BootstrapJavaScript文件 -->
        <script src="js/bootstrap.min.js"></script>
        </body>
        </html>

-  Bootstrap框架在全局样式设置做了一定的变更，不再一味追求归零，而是更注重重置可能产生问题的样式（如，body,form的margin等），保留和坚持部分浏览器的基础样式，解决部分潜在的问题，提升一些细节的体验，具体说明如下：

       移除body的margin声明

      设置body的背景色为白色

       为排版设置了基本的字体、字号和行高
 
       设置全局链接颜色，且当链接处于悬浮“:hover”状态时才会显示下划线样式

- 标题

   -   Bootstrap标题样式进行了以下显著的优化重置：

        1、重新设置了margin-top和margin-bottom的值，  h1~h3重置后的值都是20px；h4~h6重置后的值都是10px。

        2、所有标题的行高都是1.1（也就是font-size的1.1倍）,而且文本颜色和字体都继承父元素的颜色和字体。

        3、固定不同级别标题字体大小，h1=36px，h2=30px，h3=24px，h4=18px，h5=14px和h6=12px。

        在Bootstrap中为了让非标题元素和标题使用相同的样式，还特意定义了.h1~.h6六个类名

   -   一个标题后面紧跟着一行小的副标题。在Bootstrap中使用了`<small>`标签来制作副标题。这个副标题具有其自己的一些独特样式：

        1、行高都是1，而且font-weight设置了normal变成了常规效果（不加粗），同时颜色被设置为灰色（#999）。

         2、由于`<small>`内的文本字体在h1~h3内，其大小都设置为当前字号的65%；而在h4~h6内的字号都设置为当前字号的75%；

- 段落（正文文本）

    1、全局文本字号为14px(font-size)；

    2、行高为1.42857143（line-height），大约是20px(大其实他是通过LESS/SASS编译器计算出来的）；

    3、颜色为深灰色（#333）；

    4、字体为"Helvetica Neue", Helvetica, Arial, sans-serif;（font-family）

    该设置都定义在<body>元素上，由于这几个属性都是继承属性，所以Web页面中文本（包括段落p元素）如无重置都会具有这些样式效果。
  
- 强调内容

    如果想让一个段落p突出显示，可以通过添加类名“.lead”实现，其作用就是增大文本字号，加粗文本，而且对行高和margin也做相应的处理。
- 粗体

    粗体就是给文本加粗，在普通的元素中我们一般通过font-weight设置为bold关键词给文本加粗。在Bootstrap中，可以使用`<b>`和`<strong>`标签让文本直接加粗。

- 斜体

    在排版中，除了用加粗来强调突出的文本之外，还可以使用斜体。斜体类似于加粗一样，除了可以给元素设置样式font-style值为italic实现之外，在Bootstrap中还可以通过使用标签`<em>`或`<i>`来实现。

- 强调相关的类

    在Bootstrap中除了使用标签`<strong>`、`<em>`等说明正文某些字词、句子的重要性，Bootstrap还定义了一套类名，这里称其为强调类名（类似前面说的“.lead”）,这些强调类都是通过颜色来表示强调，具本说明如下：

    .text-muted：提示，使用浅灰色（#999）

    .text-primary：主要，使用蓝色（#428bca）

    .text-success：成功，使用浅绿色(#3c763d)

    .text-info：通知信息，使用浅蓝色（#31708f）

    .text-warning：警告，使用黄色（#8a6d3b）

    .text-danger：危险，使用褐色（#a94442）

- 文本对齐风格

    为了简化操作，方便使用，Bootstrap通过定义四个类名来控制文本的对齐风格： 

    .text-left：左对齐

    .text-center：居中对齐

    .text-right：右对齐

    .text-justify：两端对齐

- 列表

   - 无序列表、有序列表

        无序列表和有序列表使用方式和我们平时使用的一样（无序列表使用ul，有序列表使用ol标签），在样式方面，Bootstrap只是在此基础上做了一些细微的优化（仅在margin上作了细微调整）

   - 去点列表

         在Bootstrap中默认情况下无序列表和有序列表是带有项目符号的，但在实际工作中很多时候，我们的列表是不需要这个编号的，比如说用无序列表做导航的时候。Bootstrap通过给无序列表添加一个类名“.list-unstyled”,这样就可以去除默认的列表样式的风格。
       
        除了项目编号之外还将列表默认的左边内距也清零了。

  - 内联列表

         通过添加类名“.list-inline”来实现内联列表，简单点说就是把垂直列表换成水平列表，而且去掉项目符号（编号），保持水平显示。也可以说内联列表就是为制作水平导航而生。

  - 定义列表

         对于定义列表而言，Bootstrap并没有做太多的调整，只是调整了行间距，外边距和字体加粗效果。

 - 水平定义列表

         Bootstrap可以给`<dl>`添加类名“.dl-horizontal”给定义列表实现水平显示效果。、

         此处添加了一个媒体查询。也就是说，只有屏幕大于768px的时候，添加类名“.dl-horizontal”才具有水平定义列表效果。其实现主要方式：

        1、将dt设置了一个左浮动，并且设置了一个宽度为160px

        2、将dd设置一个margin-left的值为180px，达到水平的效果
 
        3、当标题宽度超过160px时，超过部分用三个省略号替代

- 代码

      在Bootstrap主要提供了三种代码风格：

       1、使用`<code></code>`来显示单行内联代码

       2、使用`<pre></pre>`来显示多行块代码

       3、使用`<kbd></kbd>`来显示用户输入代码

       不管使用哪种代码风格，在代码中碰到小于号（<）要使用硬编码“&lt;”来替代，大于号(>)使用“&gt;”来替代。而且对于`<pre>`代码块风格，标签前面留多少个空格，在显示效果中就会留多少个空格。建议在编写HTML标签时，就控制好。

       `<pre>`元素一般用于显示大块的代码，并保证原有格式不变。但有时候代码太多，而且不想让其占有太大的页面篇幅，就想控制代码块的大小。Bootstrap也考虑到这一点，你只需要在pre标签上添加类名“.pre-scrollable”，就可以控制代码块区域最大高度为340px，一旦超出这个高度，就会在Y轴出现滚动条。
- 表格

     - 表格行的类

         .active  .success   .info  .warning  .danger   分别对应不同的颜色

          和”.table-hover”配合使用时，Bootstrap针对这几种样式也做了相应的悬浮状态的样式设置，所以如果需要给tr元素添加其他颜色样式时，在”.table-hover”表格中也要做相应的调整。

         注意要实现悬浮状态，需要在`<table>`标签上加入table-hover类。

     -  基础表格

         在Bootstrap中，对于基础表格是通过类名“.table”来控制。如果在`<table>`元素中不添加任何类名，表格是无任何样式效果的。想得到基础表格，我们只需要在`<table>`元素上添加“.table”类名，就可以得到Bootstrap的基础表格：

          “.table”主要有三个作用：

        ☑  给表格设置了margin-bottom:20px以及设置单元内距

        ☑  在thead底部设置了一个2px的浅灰实线

        ☑  每个单元格顶部设置了一个1px的浅灰实线

     - 班马线表格

         在Bootstrap中实现让表格带有背景条纹效果，只需要在`<table class="table">`的基础上增加类名“.table-striped”即可：

         实现原理也非常的简单，利用CSS3的结构性选择器“:nth-child”来实现，所以对于IE8以及其以下浏览器，没有背景条纹效果。

         “:nth-child”匹配属于其父元素的第 N 个子元素，不论元素的类型（odd奇数，even偶数）

    - 带边框的表格

        只需要在基础表格`<table class="table">`基础上添加一个“.table-bordered”类名即可（整个表格均有边框，宽度为1px）

    - 鼠标悬浮高亮的表格

        仅需要`<table class="table">`元素上添加类名“table-hover”即可（默认鼠标悬停行呈浅灰色）

    - 紧凑型表格

         单元格没内距或者内距比其他类型的小的表格。

         只是需要在`<table class="table">`基础上添加类名“table-condensed”

         Bootstrap中紧凑型的表格与基础表格差别不大，因为只是将单元格的内距由8px调至5px。

     - 响应式表格

        Bootstrap提供了一个容器，并且此容器设置类名“.table-responsive”,此容器就具有响应式效果，然后将`<table class="table">`置于这个容器当中，这样表格也就具有响应式效果。

        Bootstrap中响应式表格效果表现为：当你的浏览器可视区域小于768px时，表格底部会出现水平滚动条。当你的浏览器可视区域大于768px时，表格底部水平滚动条就会消失。



- 基础表单

     在Bootstrap框架中，通过定制了一个类名`form-control`，也就是说，如果这几个元素使用了类名“form-control”，将会实现一些设计上的定制效果。

    1、宽度变成了100%

    2、设置了一个浅灰色（#ccc）的边框

    3、具有4px的圆角

    4、设置阴影效果，并且元素得到焦点之时，阴影和边框效果会有所变化

    5、设置了placeholder的颜色为#999

   - 水平表单

        Bootstrap框架默认的表单是垂直显示风格（标签居上，表单控件居下），但很多时候我们需要的水平表单风格（标签居左，表单控件居右）

        在Bootstrap框架中要实现水平表单效果，必须满足以下两个条件：

         1、在`<form>`元素是使用类名“form-horizontal”。

        2、配合Bootstrap框架的网格系统。（网格布局会在以后的章节中详细讲解）

         在`<form>`元素上使用类名“form-horizontal”主要有以下几个作用：

        1、设置表单控件padding和margin值。

        2、改变“form-group”的表现形式，类似于网格系统的“row”。

   - 内联表单

        只需要在`<form>`元素中添加类名“form-inline”即可。实现原理非常简单，欲将表单控件在一行显示，就需要将表单控件设置成内联块元素（display:inline-block）。
         
    - 输入框input

         单行输入框也就是input的type属性值为text。在Bootstrap中使用input时也必须添加type类型，如果没有指定type类型，将无法得到正确的样式，因为Bootstrap框架都是通过input[type=“?”](其中?号代表type类型，比如说text类型，对应的是input[type=“text”])的形式来定义样式的。

         为了让控件在各种表单风格中样式不出错，需要添加类名“form-control”

         placeholder 属性提供可描述输入字段预期值的提示信息（hint）。

  

      

  