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
```
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
            $("tr td:first-child").css("background-color","green");                 
        });            

        //Traversing--filter
        $("#btn2").click(function(){
            //tr td的第一個td，背景設lightgreen(.first())
            $("tr td:first").css("background-color","green");
            $("tr td").first().css("background-color","green");  
                                                        
        });

        $("#btn3").click(function(){
            //tr td的第一個td，背景設lightblue(.eq(0))
            $("tr td").eq(0).css("background-color","green"); 
            // $("tr td:eq(0)").css("background-color","green"); 
                                                        
        });     

        $("#btn4").click(function(){
            //filtering 的 tbody tr的奇數列綠色 .odd()，index從0開始 
            // $("tbody tr").odd().css("background-color","black");

            //child filter 的 tbody tr的偶數列綠色 nth-child(even)，index從1開始
            $("tbody tr:nth-child(odd)").css("background-color","gray");   // 要填色1 & 3列  需要使用even參數  因為CSS index從1開始

            // basic filter index從0開始 
            // $("tbody tr:odd").css("background-color","gray");
                       
        });

        $("#btn5").click(function(){  
            //filtering 的 tbody tr的偶數列黃色 .even()，index從0開始 
            //child filter 的 tbody tr的奇數列綠色 nth-child(odd)，index從1開始 
            $("tbody tr:nth-child(2n)").css("background-color","lightgreen");
            
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
```
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
            $( ".item-iv" ).next().css( "border", "solid 3px green" ); //V
        });

        $("#btn2").click(function(){               
            $( ".item-iv" ).nextAll().css( "border", "solid 2px blue" );//V,VI,VII
        }); 

        $("#btn3").click(function(){               
            $( ".item-iv" ).nextUntil(".item-vii").css( "border", "solid 2px red" );  //V,VI
        });  

        $("#btn4").click(function(){                
            $( ".item-iv" ).prev().css( "border", "solid 3px green" ); //III
        });

        $("#btn5").click(function(){               
            $( ".item-iv" ).prevAll().css( "border", "solid 2px blue" );  //III,II,I
        }); 

        $("#btn6").click(function(){               
            $( ".item-iv" ).prevUntil(".item-i").css( "border", "solid 2px red" );  //III,II
        });         
    </script>
</body>
```


# Parent & Child

# Siblings and End

# Closest

# Bootstrap5
