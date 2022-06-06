# jQuery事件繫結
事件的binding使用3種關鍵字:on,one,off，語法如下:  
```
// 繫結常態事件
selector.on(events[,selector][,data] , handler)
// 繫結一次性事件
selector.one(events[,selector][,data] , handler)
// 解除繫結事件
selector.off(events[,selector] , handler)
```

# 事先繫結
範例如下:
```
// 寫法1
$("#id").click(
  function(){
  console.log($(this).text());
  }
)

// 寫法2
$("#id").on(
  "click",
  function(){
  console.log($(this).text());
  }
)
```
> 單一事件繫結單一事件  
> 前提要求selector鎖定的指標已經存在於DOM內(例如:id,class,tag...etc)  

# 多對一繫結(多事件 to 單一處理程序)
範例如下:
```
// 多重事件寫法
$("button").on("click mouseover" , function(){
  console.log($(this).val());
})
```
> event可用空格分隔多個事件  
> selector.off()也同樣適用

# 多對多繫結(多事件 to 多處理程序)
範例如下:
```
$("#div01).on(
  {
    mouseenter: function() {...} ,
    click: function(){...} ,
    dblclick: function(){...}
  }
)
```

# 動態繫結
當元素透過JS程式產生時，因為這些元素沒有定義在原先的DOM tree內，所以先前的繫結方式就會無法binding這些元素，因此要使用動態繫結!  
範例如下:
```diff
<body> 
    <div class="container">
    <table id="idtable" class="table table-bordered table-sm" >
            <tr>
                <td>A0</td>
                <td>B1</td>
                <td>C2</td>
                <td><a href="#" class="btn btn-danger">刪除</a></td>
            </tr>
            <tr>
                <td>D3</td>
                <td>E4</td>
                <td>F5</td>
                <td><a href="#" class="btn btn-danger">刪除</a></td>
            </tr>
            <tr>
                <td>G6</td>
                <td>H7</td>
                <td>I8</td>
                <td><a href="#" class="btn btn-danger">刪除</a></td>
            </tr>
        </table>
        <input class="btn btn-primary" type="button" value="add row" id="buttonAdd" >
    </div>
    <script src="../js/jquery-3.6.0.min.js"></script>
        <script>
            //測試看看
            //按下刪除按鈕(class名稱是btn-danger)時,可以將那一筆資料刪除
            //再試試看
            //按下[add row]按鈕多新增幾筆資料
            //針對新增出來的資料,按下刪除按鈕(class名稱是btn-danger)時,還可以將那一筆資料刪除嗎???
            // $('.btn-danger').click(function () {
            //     //$(this).parent().parent().remove();
            //     // $(this).parents('tr').remove();  
            //     $(this).closest("tr").remove();                  
            // });   

            // 在a binding的func由於bubbling上升到table，使table re-bind
+            $('#idtable').on("click" , ".btn-danger" ,function () {
                // $(this).parent().parent().remove();
                // $(this).parents('tr').remove();  
+                $(this).closest("tr").remove();                  
            })


            //練習使用on繫結網頁上刪除按鈕，完成刪除動作
            
            // 刪除按鈕只能針對事先binding的元素(body上原生的物件)，所以要用動態binding!
            $('#buttonAdd').click(function () {
                $('table').append("<tr><td>X</td><td>Y</td><td>Z</td><td><a href='#' class='btn btn-danger'>刪除</a></td></tr>");                    
            });                                       
        </script>
</body>
```
