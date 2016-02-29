- 特殊性a，b，c，d     

   + 行内样式  a=1
   + b=ID选择器总数
   + c=类+伪类+属性选择器的数量
   + d=类型选择器+伪元素选择器数量（：before  /：after...）
   + 连接符和通配符不具有特殊性，即特殊性为0，0，0，0
   + 继承同样不具有特殊性，不同于0，0，0，0，**它是连0都没有**
   
			  p{ color:blue;} /* 0.0.0.1 */
			
			 *{ color:red;} /* 0.0.0.0 */

             //最终p还是显示为blue

		 	   ...
		    <style>
		    *{ color:red;}
		    .blue{ color:blue;}
		    </style>
		    
		    <body>
		    <p class="blue">这里的文字<em>hello</em></p>   // hello仍为红色，因为继承不具有任何特殊性（干不过通配符的0，0，0，0）
		    </body>
		    ...
