# jQuery事件
由於jQuery沒有addEventListener的寫法，因此只能以binding的方式定義事件處理!  
語法如下:
```
selector.eventTypeName(function(){...})
```

eventTypeName其實就是JS內的HTML DOM Events，例如: 滑鼠、鍵盤、表單、文件...etc

# jQuery Event 物件
如同JS內的Event物件定義，jQuery內的event物件屬性和方法與JS內大同小異，但有一些地方不同:
1. jQuery內沒有stopBubbling()方法(**因為無usecapture=true的引數**)  
2. which為回傳鍵盤輸入或滑鼠按鈕的代碼，滑鼠左鍵/滾輪/右鍵在JS和jQuery分別為0、1、2以及1、2、3

# 滑鼠事件
1. click() : 點擊滑鼠左鍵  
取消滑鼠左鍵語法如下:
```
$("#id").click(function(event){
  event.preventDefault();
});
```

2. contextmenu() : 按下滑鼠右鍵  
取消滑鼠右鍵語法如下:
```
$(document).contextmenu(function(event){
  event.preventDefault();
});
```

3. mousedown() : 滑鼠在選取的元素上按下時觸發
4. mouseup() : 滑鼠在選取的元素下放開時觸發
5. mouseenter() : 只有當滑鼠游標移入選取元素時才會觸發
6. mouseleave() : 只有當滑鼠游標離開選取元素時才會觸發
7. mouseover() : 當滑鼠移入選取元素&子元素時都會觸發 (觸發多次)
8. mouseout() : 當滑鼠離開選取元素&子元素時都會觸發 (觸發多次)
9. mousemove() : 每當滑鼠在選取元素&子元素上移動時都會觸發 (觸發多次)
10. hover() : 滑鼠游標移入或移出選取元素時都會觸發，hover=mouseenter+mouseleave 

語法如下:
```
selector.hover( function1 , function2 );  //第一個引數控制進入時的動作;第二個引數控制離開時的動作
```
11. index() : 回傳同層級元素的第幾個索引，從0開始計算

語法如下:
```
selector.index();
```
範例(注意優先度 mousedown > mouseup > mouseclick):
```
<body>
    <input id="idbut" type="button" value="button">
    <div>div<br><span>span</span></div>
    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        $(function(){

            // $("div").mousedown(function(){
            //     alert("div")
            // });
            // $("span").mousedown(function(){
            //     alert("span");                
            // })

            //mouseover 及 mouseenter 優先權一樣，寫前面的先觸發
            //mousedown 觸發後，mouseup 及 click不會被觸發
            //mouseup 優先權高於click            
            
            // $('#idbut').mouseover(function(){
            //     alert("mouseover");
            // });

            // $('#idbut').mouseout(function(){
            //     alert("mouseout");
            // });

            // $('#idbut').mouseenter(function(){
            //     alert("mouseenter");
            // });

            // $('#idbut').mouseleave(function(){
            //     alert("mouseleave");
            // });
            
            // $('#idbut').mousedown(function(){
            //     alert("mousedown");
            // });
            
            $('#idbut').mouseup(function(){
                alert("mouseup");
            });
            
            $('#idbut').click(function(){
                alert("click");
            });           

        })
    </script>

</body>
```

# 鍵盤事件
1. keydown() : 建盤按下時觸發，使用which可取得對應鍵盤代碼，代碼只回傳大寫(不分大小寫)，可偵測特殊鍵
2. keyup() : 鍵盤離開時觸發，使用which可取得對應鍵盤代碼，代碼只回傳大寫(不分大小寫)，可偵測特殊鍵
3. keypress() : 鍵盤按下放開時觸發，可偵測大小寫但無法偵測特殊鍵
4. text() / text("value") : 讀取 / 設定元素文字內容
5. val() / val("value") : 讀取表單第一個元素的值 / 設定表單所有元素值

範例:
```
<div class="container">
       <input  class="form-control" id="idText" type="text">
       <h1 >hello, <span id="showName"></span></h1>

    </div>
    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        //事件優先順序 keydown->keypress->keyup
            $("#idText").keydown(function(){
            console.log("keydown");
            // console.log(event.which);
        });

        $("#idText").keyup(function(){
            console.log("keyup"); 
            console.log(event.which);
            //輸入值在#showName顯示
            // let value = $(this).val();
            // $("showName").text(value);
            $("#showName").text($(this).val());
            
        });                

        $("#idText").keypress(function(){
            console.log("keypress");
            console.log(event.which);
        });               
    </script>
```

# 表單事件
1. focus() : 游標移入元素時觸發
2. blur() : 游標離開元素時觸發
3. change() : 偵測input元素內修改選取內容且游標離開選單、下拉式選單選取時都會觸發
4. submit() : 傳送表單內容到伺服器

範例:
```
<body>
    <div class="container">
        <form id="myform" action="http://192.168.37.200:8080/get.jsp"  >            
            <div class="py-2">
                <input type="text" id="idInp" name="txtName" class="form-control">
                <span id="idsp"></span>
            </div>
            <div class="py-2">
                <select class="form-control" name="" id="idSel">
                    <option value="1">台北市</option>
                    <option value="2">新竹市</option>
                    <option value="3">台中市</option>
                </select>
            </div>
            <div class="">
                <a id="idbtn" class="btn btn-info position-relative">click</a>
                <input type="submit" class="btn btn-info position-relative" value="submit">
            </div>
            <div id="demo"></div>
        </form>
    </div>

    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        //focus,blur
        $("#idInp").focus(function(){
            $(this).css("background-color","gray");
            console.log("focus"); 
            
            
        }).blur(function(){
            console.log("blur");
            $(this).css("background-color","lightcoral");
            
        }).change(function(){
            console.log("change");
        })

        //change
        $("#idSel").change(function(){
            console.log("change");
            //讀取option的值
            var v3 = $(this).index();
            var v1 = $(this).val();
            // var v2 = $(`option[value=${v1}]`).text();
            var v2 = $("select>option:selected").text();

            console.log(v3);
            console.log(v1);
            console.log(v2);

            $("#demo").text(`index=${v3} ; value=${v1} ; text=${v2}`)
                    
        });
        
        //submit
        $("#idbtn").click(function(){
                                                          
            if($("#idInp").val()==""){
                console.log("No Input!"); 
                $("#demo").text("You must enter !");
            }else{
                console.log("submit"); 
                $("form").submit();
            }
        });

        $("#myform").submit(function(event){
            console.log("submit!"); 
            // console.log(event.type);
                        
        });
    </script>
</body>
```


# 文件/視窗事件
document event : 
1. load() :頁面載入時觸發
2. unload() :頁面離開時觸發
3. ready() : DOM載入完成時觸發

window event :
1. scroll() : 滑鼠在視窗捲軸上滾動時觸發
2. resize() : 瀏覽器大小改變時觸發

範例:
```
<body>
    <figure>
        <img src="images/sport.jpg" title="戴資穎title" alt="戴資穎" style="width:300px;height: 200px;">
        <a href="https://tw.news.yahoo.com/">
            <img src="images/sport.jpg"  style="width:300px;height: 200px;">
        </a>
        <figcaption>戴資穎</figcaption>
    </figure>
    <p> 請自行準備一篇夠長的段落文字</p>
    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        $(window).scroll(function(){
            console.log("scrolling");
        });

        $(window).resize(function(){
            console.log("resizeing");                
        });
    </script>
</body>
```


# CSS - 轉場效果
transition可改變網頁呈現效果，中間的過程就是轉場。  
以下為常用屬性:
> transition-property : 定義轉場屬性效果的屬性名稱，例如:寬度、背景、顏色...etc  
> transition-duration : transition執行時間，單位為秒(s)或毫秒(ms)  
> transition-timing-function : 使用加速度曲線來表示動畫變換的速度  
> transition-delay : 開始執行之前的延遲時間，預設為0秒  

# CSS - 物件對齊
以下兩種CSS屬性能夠將div內的物件對齊:
> justify-content: center (置中對齊)  
> align-items: center (若div內的物件不等高，會依div中線對齊)  

# CSS - 自動填滿
object-fit能夠控制置換元素的內容填入大小，引數有:
> fill : 預設，強制變形至CSS所定義的元素寬高，不管原檔案比例  
> cover : 填滿元素高度及寬度，並維持原比例，通常會有一部分內容被截掉  
> none : 不做任何大小與比例調整  

# 特殊字體
來源: https://fontawesome.com/  
step1 : Get Started  
step2 : Other Ways to Use頁面內，右上角Download  
step3 : 點擊 FreeForWeb 進行下載
step4 : 解壓縮至html文件資料夾內  
![Image](https://github.com/EnasVen/jQuery/blob/main/fontDownload.png)

免費icon如果要使用，可以點擊上方導覽列的icon圖示，接著點擊最右邊的free and open-source icons進入  
後續便依照使用者需求進行搜尋與下載!  

