# Selector
用來選取網頁內的元素，以陣列的型態封裝成jQuery物件回傳。  
jQuery主要分為以下2種:
1. CSS選擇器
  - 套用原生CSS selector語法產生的jQuery選擇器
2. jQuery自訂選擇器
  - 參考 [https://api.jquery.com/category/seletors/](https://api.jquery.com/category/selectors/)  
  - 須注意標籤內若包含 Selectors > jQuery Extensions則代表這種選擇器是jQuery獨有的寫法!  


# Basic Selector
基礎選擇器為CSS語法衍生:
> \* : ```$("*")``` 選取所有元素  
> element : ```$("div")``` 選取所有指定tag name元素  
> .class : ```$(".myClass")``` 選取所有指定class name元素  
> \#id : ```$("#myDiv")``` 選取所有指定id元素  
> [tag,id].class : ```$("div.a1")``` 複合型選取方式　　

# Form Selector
以 : 進行type選取  
> $(":button") : 選取type為butto以及標籤是button的元素  
> $(":checkbox") :  選取type為checkbox的所有元素  
> $(":checked") : 選取屬性為checked(被勾選)的所有元素，注意除了input標籤之外，select標籤內的option selected也算!  
> $(":selected") : 選取屬性為selected的所有元素，只計算selected底下有選擇的options
> $(":disabled") : 選取屬性為disable的所有元素  
> $(":enable") : 選取屬性為enable的所有元素  
> $(":file") : 選取type為file的所有元素  
> $(":image") : 選取type為image的所有元素  
> $(":input") : 選取表單中的所有元素  
> $(":password") : 選取type為password的所有元素  
> $(":radio") : 選取type為radio的所有元素  
> $(":reset") : 選取type為reset的所有元素  
> $(":submit") : 選取type為submit的所有元素  
> $(":text") :  選取type為text的所有元素  


# Attribute Selector
透過屬性名稱與屬性值來做選取:  
> $("tag[attr]") : 選擇有attr屬性的任何tagt元素  
> $("tag[attr=value]") : 選擇attr屬性值為value的所有tag元素  
> $("tag[attr!=value]") : 選擇attr屬性值不為value的所有tag元素 
> $("tag[attr^=value]") : 選擇attr屬性值開頭為value的所有tag元素 
> $("tag[attr*=value]") : 選擇attr屬性值內包含value的所有tag元素 
> $("tag[attr$=value]") : 選擇attr屬性值以value結尾的所有tag元素 
> $("tag[attr|=value]") : 選擇attr屬性值為value或value-的所有tag元素
> $("tag[attr1][attr2$=value]") : 複合是寫法，選擇attr1屬性值內，所有attr2屬性值為value的所有tag元素

 
# Hierarchy Selector
透過parent - child的方式來找到元素位置  
> $("parent > child") : 例如: ```$("#div1 > a")```選取id=#div1元素下一層級的a元素，須注意這個方式只搜尋最近的下一層級元素，非多重搜尋!  
> $(descendant selector) : 例如: ```$("#div1 a")```選取id=#div1元素下，所有層級內包含a元素之集合  
> $(prev + next) : 例如: ```$("#div1+a")```選取#div1同一層級相鄰的a元素  
> $(prev~siblings) :例如: ```$("#div1~a")```選取#div1同一層級的所有a元素  

# Child Filter
為原生CSS selector寫法:  
> $(tag tag:first-child) : 例如: ```$("div p:first-child")```選取每個div元素底下的第一個p元素  
> $(tag tag:last-child) : 例如: ```$("div p:last-child")```選取每個div元素底下的最後一個p元素  
> $(tag tag:nth-child(n)) : 例如: ```$("div p:nth-child(n)")```選取每個div元素底下的第n個p元素  
> $(tag tag:nth-child(2n)) : 例如: ```$("div p:nth-child(2n)")```選取每個div元素底下的第2,4,6...個p元素。注意索引值要>1，所以取值必須從1開始  
> $(tag tag:nth-child(2n+1)) : 例如: ```$("div p:nth-child(2n+1)")```選取每個div元素底下的第1,3,5...個p元素，注意索引值要>1，所以取值必須從0開始  
> $(tag tag:only-child) : 例如: ```$("div p:only-child")```選取div元素下只有一個p的元素  

範例，包含奇偶數填色:
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
    <input type="button" id="btn2" value=":last-child">
    <input type="button" id="btn3" value=":nth-child(2)">
    <input type="button" id="btn4" value=":only-child">
    <hr>
    <input type="button" id="btn5" value=":nth-child(even)">
    <input type="button" id="btn6" value=":nth-child(odd)">
    <input type="button" id="btn7" value=":nth-child(2n)">
    <input type="button" id="btn8" value=":nth-child(2n+1)">
    <input type="button" id="btn9" value=":nth-child(3n+1)">

    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        $("#btn1").click(function(){                 
            $("tr td:first-child").css("background-color","yellow");                
        });

        $("#btn2").click(function(){                
            $("tr td:last-child").css("background-color","orange");
        });

        $("#btn3").click(function(){               
            $("tr td:nth-child(2)").css("background-color","lime");
        });

        $("#btn4").click(function(){               
            $("thead tr:only-child").css("background-color","fuchsia");
        });

        //child filter selector,選擇器由1開始計數
        $("#btn5").click(function(){
            //tbody tr的偶數列綠色 nth-child(even)                 
            $("tbody tr:nth-child(even)").css("background-color","green");                
        });

        $("#btn6").click(function(){  
            //tbody tr的奇數列黃色 nth-child(odd)               
            $("tbody tr:nth-child(2n+1)").css("background-color","firebrick"); 
        });

        $("#btn7").click(function(){                                                        
            //tbody的2n列藍色 :nth-child(2n) 偶數
            //2n的n,n從1開始
            $("tbody tr:nth-child(2n)").css("background-color","LightCoral"); 
                
        });  

        $("#btn8").click(function(){
            //tbody的2n+1列紅色 :nth-child(2n+1) 奇數
            //(2n+1)的n ,n從0開始
            $("tbody tr:nth-child(2n+1)").css("background-color","LightGreen");                 
        }); 

        $("#btn9").click(function(){
            //第1,4...列文字顏色設為桃紅色(fuchsia) :nth-child(3n+1)
            $("tbody tr:nth-child(3n+1)").css("background-color","pink");  

        });                         
    </script>    
</body>
```

# Contant Filter
根據元素內容做篩選:
> $(tag:contains(**text**)) : 例如: ```$("p:contains('ABC')")```選取所有內容包含"ABC"文字的p元素，注意引數必須為字串!  
> $(tag:has(**selector**)) : 例如: ```$("div:has(p)")```選取含有p元素的div元素，注意引數必須為選擇器!  
> $(tag:empty) : 例如: ```$("p:empty")```選取內容為空的p元素，注意單一標籤無內容，因此也會被選到!  
> $(tag:parent) : 例如: ```$("p:parent")```選取含有子元素或者內容文字的p元素，注意單一標籤不會被選到!  

# Basic Filter
透過基礎索引來依照給定位置選取元素:
> $(tag:eq()) : 例如: ```$("td:eq(2)")```選取第3個td元素，注意由0開始算!  
> $(tag:lt()) : 例如: ```$("td:lt(4)")```選取前4個td元素，注意不包含指定數! i.e. [0,4)  
> $(tag:gt()) : 例如: ```$("td:gt(4)")```選取第3個td元素，注意不包含指定數! i.e. (4,n]  
> $(tag:even()) : 例如: ```$("tr:even")```選取索引值(index)是偶數列的tr元素  
> $(tag:odd()) : 例如: ```$("tr:odd")```選取索引值(index)是奇數列的tr元素  
> $(tag:fist()) : 例如: ```$("tr:first")```選取第一個tr元素  
> $(tag:last()) : 例如: ```$("tr:last")```選取最後一個tr元素  
> $(tag:header()) : 例如: ```$(":header")```選取h1~h6的HTML tag  
> $(tag:animated()) : 例如: ```$("div:animated")```選取正在被animation的div元素  
> $(tag:not(**selector**)) : 例如: ```$("input:not(:checked)")```選取沒有被checked的input元素，注意selector不用加""!  

範例(注意奇偶數的填色):
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
                <td class="nobg">Java</td>
                <td>Static</td>
                <td>1995</td>
            </tr>
            <tr>
                <td>Ruby</td>
                <td>Dynamic</td>
                <td>1993</td>
            </tr>
            <tr>
                <td class="nobg">JavaScript</td>
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
    <div>
        <label>hobbys:</label>
        <input type="checkbox" name="hobby" id="checkbox1" value="1" />
        <label>reading</label>
        <input type="checkbox" name="hobby" id="checkbox2" value="2" />
        <label>play</label>
        <input type="checkbox" name="hobby" id="checkbox3" value="3" checked="checked" />
        <label>sport</label>
        <input type="checkbox" name="hobby" id="checkbox4" value="4" />
        <label>movie</label>
    </div>
    <hr>

    <input type="button" id="btn1" value=":eq(3)">
    <input type="button" id="btn2" value=":lt(2)">
    <input type="button" id="btn3" value=":td:even">
    <input type="button" id="btn4" value=":td:odd">
    <input type="button" id="btn5" value=":first">
    <input type="button" id="btn6" value=":header">
    <input type="button" id="btn7" value=":not()">

    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        $(function () {
            $("#btn1").click(function () {
                $("td:eq(3)").css("background-color", "yellow");
            });

            $("#btn2").click(function () {
                $("td:gt(2)").css("background-color", "green");
            });

            $("#btn3").click(function () {
                $("td:even").css("background-color", "aqua");
            });

            $("#btn4").click(function () {
                $("td:odd").css("background-color", "fuchsia");
            });

            $("#btn5").click(function () {
                $("td:first").css("background-color", "lime");
            });

            $("#btn6").click(function () {
                $(":header").css("background-color", "blue");
            });

            $("#btn7").click(function () {
                //將td標籤沒有 nobg 類別的背景設為黃色
                $("td.nobg").css("background-color", "pink");
                // $("td:not(.nobg)").css("background-color","blue");
            });  //click                
        });
    </script>
</body>
```
