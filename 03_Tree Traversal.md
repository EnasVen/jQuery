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
