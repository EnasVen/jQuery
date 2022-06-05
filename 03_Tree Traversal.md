# Filtering
基於Selector chain 的語法，我們可以用action()的方式來達成指定位置索引:
> first() : ```$("li").first()``` : 回傳第一個li元素  
> last() : ```$("li").t()``` : 回傳最後一個li元素  
> eq(**index**) : ```$("li").eq(2)``` : 回傳第2個li元素，注意index從0開始算!  
> even() : ```$("li").even()``` : 回傳偶數列li元素  
> odd() : ```$("li").odd()``` : 回傳奇數列li元素  
> slice(start[,end]) : ```$("li").slice(2,4)``` : 回傳第[2,4)，也就是第3和第4個li元素  
> not(**selector**) : ```$("li").not(".item")``` : 回傳所有class!="item"的li元素  
> has(**selector**) : ```$("ui").has("li")``` : 回傳含有li元素的所有ul元素  
> filter(**selector**) : ```$("li").filter(".item")``` : 回傳所有class="item"的li元素 

範例:
```diff
<body>
    <h2>languages table</h2>
    <table id="languages">
        <thead>
            <tr>
                <th>Language</th>
                <th>Type</th>
                <th>Invented</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Java</td>
                <td>Static</td>
                <td>1995</td>
            </tr>
            <tr>
                <td>Ruby</td>
                <td>Dynamic</td>
                <td>1993</td>
                </tr>
            <tr>
                <td>JavaScript</td>
                <td>Dynamic</td>
                <td>1995</td>
            </tr>
            <tr>
                <td>C++</td>
                <td>Static</td>
                <td>1983</td>
            </tr>
        </tbody>
    </table>
    <hr>

    <input type="button" id="btn1" value=":first-child">    
    <input type="button" id="btn2" value=".first()">
    <input type="button" id="btn3" value=".eq(0)">
    <input type="button" id="btn4" value=".odd()">    
    <input type="button" id="btn5" value=".even()">   

    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        //child Selector
        $("#btn1").click(function(){
            //每個tr的第一個td，背景設yellow(:first-child)                 
+            $("tr td:first-child").css("background-color","green");                 
        });            

        //Traversing--filter
        $("#btn2").click(function(){
            //tr td的第一個td，背景設lightgreen(.first())
+            $("tr td:first").css("background-color","green");
+            $("tr td").first().css("background-color","green");  
                                                        
        });

        $("#btn3").click(function(){
            //tr td的第一個td，背景設lightblue(.eq(0))
+            $("tr td").eq(0).css("background-color","green"); 
            // $("tr td:eq(0)").css("background-color","green"); 
                                                        
        });     

        $("#btn4").click(function(){
            //filtering 的 tbody tr的奇數列綠色 .odd()，index從0開始 
            // $("tbody tr").odd().css("background-color","black");

            //child filter 的 tbody tr的偶數列綠色 nth-child(even)，index從1開始
+            $("tbody tr:nth-child(odd)").css("background-color","gray");   // 要填色1 & 3列  需要使用even參數  因為CSS index從1開始

            // basic filter index從0開始 
            // $("tbody tr:odd").css("background-color","gray");
                       
        });

        $("#btn5").click(function(){  
            //filtering 的 tbody tr的偶數列黃色 .even()，index從0開始 
            //child filter 的 tbody tr的奇數列綠色 nth-child(odd)，index從1開始 
+           $("tbody tr:nth-child(2n)").css("background-color","lightgreen");
            
        });                                                                     
    </script>    
</body>
```

# Next & Prev
next() action包含以下種類:
> next([selector]) : 回傳目前元素同一層中的下一個元素(這個下一個元素可以使用jQuery selector達成條件搜尋)  
> nextAll([selector]) : 回傳目前元素同一層中後面的所有元素  
> nextUntil([selector] , [filter]) : 回傳目前元素同一層中，符合filter條件且直到selector之前的所有元素  

prev() action包含以下種類:
> prev([selector]) : 回傳目前元素同一層中的前一個元素(這個前一個元素可以使用jQuery selector達成條件搜尋)  
> prevAll([selector]) : 回傳目前元素前一層中後面的所有元素  
> prevUntil([selector] , [filter]) : 回傳目前元素同一層中，符合filter條件且直到selector之後的所有元素  

next和prev範例:
```diff
<body>body(grandparent)
    <ul class="level-1" style="width:500px" >ul(direct parent)
        <li class="item-i">I</li>
        <li class="item-ii">II</li>
        <li class="item-iii">III</li>
        <li class="item-iv">IV(self)
          <ul class="level-2">ul(children)
            <li class="item-a">A</li>            
          </ul>
        </li>
        <li class="item-v">V</li>
        <li class="item-vi">VI</li>
        <li class="item-vii">VII</li>       
      </ul>
    <hr>
    <input type="button" id="btn1" value="next()">
    <input type="button" id="btn2" value="nextAll()"> 
    <input type="button" id="btn3" value="nextUntil()"><br>
    <input type="button" id="btn4" value="prev()">
    <input type="button" id="btn5" value="prevAll()"> 
    <input type="button" id="btn6" value="prevUntil()">

    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        $("#btn1").click(function(){                
+            $( ".item-iv" ).next().css( "border", "solid 3px green" ); //V
        });

        $("#btn2").click(function(){               
+            $( ".item-iv" ).nextAll().css( "border", "solid 2px blue" );//V,VI,VII
        }); 

        $("#btn3").click(function(){               
+            $( ".item-iv" ).nextUntil(".item-vii").css( "border", "solid 2px red" );  //V,VI
        });  

        $("#btn4").click(function(){                
+            $( ".item-iv" ).prev().css( "border", "solid 3px green" ); //III
        });

        $("#btn5").click(function(){               
+            $( ".item-iv" ).prevAll().css( "border", "solid 2px blue" );  //III,II,I
        }); 

        $("#btn6").click(function(){               
+            $( ".item-iv" ).prevUntil(".item-i").css( "border", "solid 2px red" );  //III,II
        });         
    </script>
</body>
```


# Parent & Child
parent() action包含以下種類:
> parent[selector]) : 回傳目前元素的上一層(selector)元素(父元素)，注意不包含本身!  
> parents([selector]) : 回傳目前元素上面所有層級(selector)的元素，直到html元素  
> parentsUntil([selector] , [filter]) : 回傳目前元素的上面所有層級，符合filter條件且直到selector之下的所有層級元素

parent範例:
```diff
head>
    <meta charset="UTF-8">
    <title>04parentTraversing.html</title>
    <style>
        .level-1 * { 
            display: block;
            border: 2px solid lightgrey;
            color: lightgrey;
            padding: 5px;
            margin: 15px;
        }
        ul .item-b{
            border:2px dotted orchid;           
        }
    </style>
</head>
<body>body
    <ul class="level-1" style="width:500px" >ul
        <li class="item-i">I</li>
        <li class="item-ii">II
          <ul class="level-2">ul
            <li class="item-a">A</li>
            <li class="item-b">B(self)
                <ul class="level-3">ul
                    <li class="item-1">1</li>
                </ul>
            </li>
            <li class="item-c">C</li>
          </ul>
        </li>       
      </ul>
      <hr>
    <input type="button" id="btn1" value="parent()">
    <input type="button" id="btn2" value="parents()">
    <input type="button" id="btn3" value="parentsUntil()">
    <input type="button" id="btn4" value="closest()"> 

    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        $("#btn1").click(function(){
+            $(".item-b").parent().css( "border", "solid 2px red" );
        });

        $("#btn2").click(function(){
+            // $(".item-b").parents("ul").css( "border", "solid 2px green" ); //只有ul
+            $(".item-b").parents().css( "border", "solid 2px green" );  //ul,li,body,html              
        });

        $("#btn3").click(function(){    
+            $( ".item-b" ).parentsUntil('body').css( "border", "solid 2px blue" );  //body以下即ul,li           
        });

        $("#btn4").click(function(){ 
            $(".item-b").closest("li").css( "border", "solid 2px fuchsia" ); 
            //closest("ul")
        });           
    </script>
</body>
```

child() action包含以下種類:
> children[selector]) : 回傳目前元素的下一層(selector)元素(子元素)，注意只找一層!  
> find(selector) : 回符合selector的所有層級子元素  

child範例:
```diff
<head>
    <meta charset="UTF-8">
    <title>05descendantsTraversing.html</title>
    <style>
        .level-1 * { 
            display: block;
            border: 2px solid lightgrey;
            color: lightgrey;
            padding: 5px;
            margin: 15px;
        }
        ul .item-ii{
            border:2px dotted orchid;
        }
    </style>
</head>
<body>body(grandparent)
    <ul class="level-1" style="width:500px" >ul(direct parent)
        <li class="item-i">I</li>
        <li class="item-ii">II(self)
          <ul class="level-2">ul(children)
            <li class="item-a">A</li>
            <li class="item-b">B
                <ul class="level-3">
                    <li class="item-1">1</li>                    
                </ul>
            </li>
            <li class="item-c">C</li>
          </ul>
        </li>       
      </ul>
      <hr>
      <input type="button" id="btn1" value="children()">
    <input type="button" id="btn2" value="find('li')">
    <input type="button" id="btn3" value="find('*')">
   

    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        $("#btn1").click(function(){
+            $( "ul .item-ii" ).children().css( "border", "solid 2px red" );  //ul 
+            // $( "ul .level-2" ).children().css( "border", "solid 2px red" );  //多個li,只找一層

            //.level-2的children是.item-a,.item-b,.item-c多個兒子         
        });

        $("#btn2").click(function(){                
            $( "ul .item-ii" ).find("li").css( "border", "solid 2px green" ); //以下所有li
            // $( "ul .item-ii" ).find("ul").css( "border", "solid 2px green" ); //以下所有ul
        });

        $("#btn3").click(function(){               
            $( "ul .item-ii" ).find("*").css( "border", "solid 2px blue" );//以下所有li,ul
        });         
    </script>
</body>
```

# Siblings and End
此二actions定義如下:
> siblings([selector]) : 回傳自己以外同層級的所有元素
> end() : 結束目前chain搜尋的所有過濾操作，將符合的選擇器返回到先前狀態!(回到$符號)

siblings和end範例
```diff
<head>
    <meta charset="UTF-8">
    <title>06siblingendTraversing.html</title>
    <style> 
            .level-1 * { 
                display: block;
                border: 2px solid lightgrey;
                color: lightgrey;
                padding: 5px;
                margin: 15px;
            }       
            .item-iv{
                border:2px dotted orchid  ;
            }
        </style>
    
</head>
<body>
    <ul class="level-1" style="width:500px" >ul(direct parent)
        <li class="item-i">I</li>
        <li class="item-ii">II</li>
        <li class="item-iii">III</li>
        <li class="item-iv">IV(self)
            <ul class="level-2">ul(children)
                <li class="item-a">A</li>            
            </ul>
        </li>
        <li class="item-v">V</li>
        <li class="item-vi">VI</li>
        <li class="item-vii">VII</li>       
    </ul>
    <hr>
    <input type="button" id="btn1" value="siblings()">
    <input type="button" id="btn2" value="end()">

    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        $("#btn1").click(function(){
+            $( ".item-iv" ).siblings().css( "border", "solid 2px aqua" );  //I,II,II,V,VI,VII             
        });

        $("#btn2").click(function(){
            $( "ul.level-1" )
                .find(".item-a")
                .css( "border", "solid 2px blue" )
+                .end()
                .find(".item-ii")
                .css("border","solid 2px red");         
        });
    </script>
</body>
```


# Closest

# Bootstrap5
