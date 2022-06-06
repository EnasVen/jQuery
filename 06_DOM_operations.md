# 讀取與修改
> 讀取/設定元素文字內容(無解譯HTML語法) : text() / text("value")  
> 讀取/設定元素文字內容(可解譯HTML語法) : html() / html("value")  
> 讀取首個元素的值/設定表單所有元素的值 : val() / val("setValue")  

# 讀取、設定與刪除屬性
> 讀取 : attr("name") , prop("name")  
> 設定 : attr("name" , "value") , prop("name" , "value")  
> 刪除屬性 : removeAttr("name") , removeProp("name")  



# attr vs prop
對於HTML元素本身就帶有的固有屬性使用attr()及prop()讀取和設定，(google HTML spec)  
對於checked，selected，disabled 使用prop讀取和設定，使用attr()讀取為字串，使用prop()讀取為true 或 false  
固有屬性和checked用removeAttr,自定屬性用removeProp  
checked不管給啥，console.log都是顯示checked，無checked用attr讀取就是回傳undefined!  

# 元素處理
元素的新刪修包含以下方法:
1. remove() : 刪除選取元素與其內容  
2. empty() : 刪除選取元素下的子元素，不含選取元素，只刪除選取元素內容  
3. append(content) : 在選取元素內容尾端插入內容  
4. prepend(content) : 在選取元素內容前端加入內容 
5. appendTo(target) : 把選取元素加入指定目標尾端
6. prependTo(target) : 把選取元素加入指定目標前端
```
$("#btnappTo").click(function(){               
    $("<b>appendTo</b>").appendTo(".inner");
    // $("appendTo").appendTo(".inner"); //錯誤的寫法,因為無法變成jQuery物件
});

$("#btnpreTo").click(function(){               
    $("<b>prependTo</b>").prependTo(".inner");
});
```
7. after(content) :在選取元素外部後面插入內容
8. before(content) : 在選取元素外部前面插入內容
9. insertAfter(target) : 把選取元素加入指定目標外部後面
10. insertBefore(target) : 把選取元素加入指定目標外部前面
```
$("#btninsAfter").click(function(){
    $("<b>insertAfter</b>").insertAfter(".inner");               
});

$("#btninsBefore").click(function(){                
    $("<b>insertBefore</b>").insertBefore(".inner");
});
```

示意圖如下:  
![Image](https://github.com/EnasVen/jQuery/blob/main/appendRelated.png)  

# Selector 的 each
類似迴圈的方式處理選擇器的類物件，語法範例如下:
```
$(JSselector).each(function(index,element){...})
```
其中index表示元素索引值，從0開始;element表示回傳的元素(JS物件)
範例如下:
```
<script>
    $("#btn1").click(function(){                             
        $("li").each(function(index,element){
            console.log($(this).text());
            console.log($(element).text()); 
            $("#demo").append(`<li>${$(this).text()}</li>`);                                               
        });                  
    });
</script>
```

# jQuery 的 each
1. jQuery.each(array , callback) : 
    - 針對陣列中每個元素來處理，也可針對類陣列的資料型別處理  
    - callback為 function(Integer index , Object value)，index為iterable物件的元素順序 
2. jQuery.each(object , callback) :
    - callback為 function(String propertyName , Object valueofProperty)

範例: 
```diff
<body>
    <div id="msg"></div>
    <script src="../js/jquery-3.6.0.min.js"></script>
   <script>
       //  印出陣列內每一個元素的指標與內容
       let ary=["item1", "item2", "item3"];
+        $.each(ary,function(index,value){
            console.log(index+":"+value);
        });

        var data = {"emps":[
                      {"name":"Tom","workYears":3,"salary":35000},
                      {"name":"Jack","workYears":5,"salary":40000},
                      {"name":"Mary","workYears":7,"salary":45000}
                   ]};
        // 印出JSON物件內的每一個元素
+        $.each(data,function(index,value){
            console.log(index);
            console.log(value);
            $.each(value,function(index2,value2){
                // console.log(value2);
                n = value2.name;
                wy=value2.workYears;
                sl=value2.salary;
                $("#msg").append(`<li>${n},${wy},${sl}</li>`)
            })
        })
   </script> 
</body>
```
上面的範例內，第2個範例，console.log會印出JSON物件的propertyName，也就是emps這個屬性，並以字串表示。  
而下一個console.log則會印出屬性值，也就是包含3個object物件的list!  
