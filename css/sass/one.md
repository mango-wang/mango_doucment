1
 1.1 变量  

        声明变量的符号“$”
        eg. $highlight-color: #F90;
 1.2 默认变量
 
      sass的默认变量仅需要在值后面加上!default即可。
      
          $baseHeight:        2;
          $baseHeight:        1.6 !default;
          body{
              line-height: $baseHeight; 
          }
      编译出来 line-height :2
 1.3 局部变量和全局变量
 
      $color: blue !default;//定义全局变量(在选择器、函数、混合宏...的外面定义的变量为全局变量)
      .box1 {
        color: $color;//调用全局变量
      }
      p {
        $color: red;//定义局部变量
        a {
          color: $color;//调用局部变量
        }
      }
      .box2 {
        color: $color;//调用全局变量
      }  
      a 标签为红色  
      如想影响 !global 参数  
 1.4 嵌套-选择器嵌套
   
     所谓选择器嵌套指的是在一个选择器中嵌套另一个选择器来实现继承，从而增强了sass文件的结构性和可读性。  
     在选择器嵌套中，可以使用&表示父元素选择器
     
         #top_nav{
           line-height: 40px;
           li{
             float:left;
           }
           a{
             padding: 0 10px;
             color: #fff;
          
             &:hover{
               color:#ddd;
             }
           }
         } 
       编译结果  
       
       #top_nav{
         line-height: 40px;
       }
       #top_nav li{
           float:left;
       }
       #top_nav a{
           padding: 0 10px;
           color: #fff;
       }
       #top_nav a:hover{
             color:#ddd;
       }
 1.5 嵌套-属性嵌套        
 
     所谓属性嵌套指的是有些属性拥有同一个开始单词，如border-width，border-color都是以border开头。实例如下：
      
          .box2 {
            border: {
              style: solid;
              left: {
                width: 4px;
                color: #888;
              }
              right: {
                width: 2px;
                color: #ccc;
              }
            }
          }
 2 混合声明和调用  
 
        sass中使用@mixin声明混合，可以传递参数，参数名以$符号开始，多个参数以逗号分开，也可以给参数设置默认值。声明的@mixin通过@include来调用。
 2.1 无参数mixin
 
             @mixin center-block {
                 margin-left:auto;
                 margin-right:auto;
             }
             
           在混合宏“center-block”中定义了无参数。
           
           调用混合宏：
           
               .box2{
                   @include center-block;
               }
           
           编译出来的 CSS:
           
               .box2{
                   margin-left:auto;
                   margin-right:auto;
               }
 2.2 有参数mixin
 
      @mixin opacity($opacity:50) {
       opacity: $opacity / 100;
       filter: alpha(opacity=$opacity);
     }
     
     
         .opacity-80{
           @include opacity(80); //传递参数
         }
 2.3 多个参数mixin
     
           @mixin horizontal-line($border:1px dashed #ccc, $padding:10px){
              border-bottom:$border;
              padding-top:$padding;
              padding-bottom:$padding;  
          }
 3.继承
     
      使用sass的时候，最后一个减少重复的主要特性就是选择器继承。基于Nicole Sullivan面向对象的css的理念，选择器继承是说一个选择器可以继承为另一个选择器定义的所有样式。这个通过@extend语法实现
      
      .error {
        border: 1px red;
        background-color: #fdd;
      }
      .seriousError {
        @extend .error;
        border-width: 3px;
      }
 
 4.特性
 
 4.1 选择器占位符%placeholder
 
 4.2 数据类型
 
      
    数字（例如 1.2、13、10px）
    文本字符串，无论是否有引号（例如 "foo"、'bar'、baz）
    颜色（例如 blue、#04a3f9、rgba(255, 0, 0, 0.5)）
    布尔值（例如 true、false）
    空值（例如 null）
    值列表，用空格或逗号分隔（例如 1.5em 1em 0 2em、Helvetica, Arial, sans-serif）
    SassScript 还支持所有其他 CSS 属性值类型， 例如 Unicode 范围和 !important 声明。 然而，它不会对这些类型做特殊处理。 它们只会被当做不带引号的字符串看待。
 4.3 字符串
 
 
    带引号的字符串，例如 "Lucida Grande" 或 'http://sass-lang.com'；
    不带引号的字符串，例如 sans-serif 或 bold。
 4.4 值列表
 
 5 数字运算
 
 5.1 所有数据类型都支持等式运算 (== and !=)。 另外，每种数据类型也有其支持的特殊运算符。
 
 5.2 除法运算和
 
 5.3 颜色运算
 
         p {
           color: #010203 * 2;
         }
 5.4 + 运算符可以用来连接字符串：
 
     p {
       cursor: e + -resize;
     }
     
         p {
           cursor: e-resize; }
 6 判断循环
 
 6.1 @if判断
      
    除非必要，不然不需要括号；
    务必在 @if 之前添加空行；
    务必在左开大括号( { )后换行；
    @else 语句和它前面的右闭大括号( } )写在同一行；
    务必在右闭大括号( } )后添加空行，除非下一行还是右闭大括号( } )，那么就在最后一个右闭大括号( } )后添加空行。
 
 6.2 三目运算判断
   
   
    @if($condition, $condition_true, $condition_false)，
    三个参数分别表示：条件，条件为真的值，条件为假的值。
 6.3 for循环  
 
    
    @for $i from through
    @for $i from to
    $i 表示变量 start 表示起始值 end 表示结束值

    这两个的区别是关键字 through 表示包括 end 这个数，而 to 则不包括 end 这个数。
    
         @for $i from 1 through 3 {
          .item-#{$i} { width: 2em * $i; }
        }
 6.4 each循环
    
      @each 循环就是去遍历一个列表，然后从列表中取出对应的值。
     
     @each 循环指令的形式： @each $var in < list > 
 6.5 while循环
 
      @while 指令也需要 SassScript 表达式（像其他指令一样），并且会生成不同的样式块，直到表达式值为 false 时停止循环。这个和 @for 指令很相似，只要 @while 后面的条件为 true 就会执行。
      