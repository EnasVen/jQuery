# CSS樣式修改
1. 讀取樣式: $(selector).css("name")
2. 設定樣式: $(selector).css("name","value") or $(selector).css("name") = "value"
```
// 可設定遞增遞減
$(".block").css("width" , "+=15px");

// 多重設定
$(".block").css("width":"15px" , "height":"10px" , "background-color":"red");
```

# jQuery Dimensions
利用dimension方法和屬性可以設定物件尺寸和瀏覽器視窗:  
1. innerWidth([value]) : 元素包含padding寬度
2. innerHeight([value]) :元素包含padding高度
3. outerWidth([value]) :元素包含padding和border高度
4. outerHeight([value]) :元素包含padding和border高度
5. outerWidth([boolean]) :是否包含元素margin高度，deault true
6. outerHeight([boolean]) :是否包含元素margin高度，deault true
 
![Image](https://github.com/EnasVen/jQuery/blob/main/dimension.png)  

width([value])以及height([value])可以讀取或設定物件的寬/高  
須注意設定瀏覽器寬or高時，要使用.width()/.height()而不能用.css()  
這是因為透過jQuery selector得到的window為物件，而非jQuery selector!
```
$(window).width() //正確讀取瀏覽器寬度方式
$(window).css("width") //錯誤讀取瀏覽器寬度方式
```

使用resize()方法使物件在瀏覽器內保持水平置中:
```
<body>
    <div id="div1">
            <img id="image1" src="images/tesla1.jpg">
    </div>
    
    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        move_div();

        //當視窗放大或縮小時呼叫move_div的函式
        //讓div1置中
        $(window).resize(adjustDiv).resize(move_div);

        function move_div() {
            let windowHeight = $(this).height();
            let windowWidth = $(this).width();
            let objHeight = $("#div1").height();
            let objWidth = $("#div1").width();

            let top = (windowHeight-objHeight)/2;
            let left = (windowWidth-objWidth)/2;

            $("#div1").css("top",top).css("left",left);
        }   

        function adjustDiv() {
            let windowHeight = $(this).height();
            let windowWidth = $(this).width();
            let objHeight = $("#div1").height();
            let objWidth = $("#div1").width();

            let topRatio = Math.floor(100*objHeight/windowHeight);
            let leftRatio = Math.floor(100*objWidth/windowWidth);

            $("#div1").css("width",`${leftRatio}%`).css("height",`${topRatio}%`);
        }
    </script>
</body>
```

# 視窗卷軸位置
使用以下三種方法讀取或設定卷軸水平/垂直位置以及元素的相對座標:
1. scrollTop([value]) : 讀取或設定卷軸垂直位置
2. scrollLeft([value]) : 讀取或設定卷軸水平位置
3. offset() : 讀取指定元素在HTML上的相對座標，並回傳含有top,left屬性的物件!  

# 捲動事件(scroll)
可視範圍單位:
vh/vw: view height/width，代表螢幕可視範圍高度/寬度百分比，100vh/vw即代表整個螢幕高/寬  
下面的範例實作如何偵測當前捲軸高度，並在上方以紅色bar條顯示捲軸進度:
```
<head>
    <style>
        body{
            /* 設定三倍可視高度 */
            height: 300vh; 
        }
        .read_progress{
            position: fixed;
            left:0;
            right:0;
            top:0;
            height: 20px;
            background: rgba(0,0,0,.3);
        }
        .read_progress_bar{
            height: 20px;
            background: red;
            width: 0%;
        }
    </style>
</head>
<body>
    <div class="read_progress">
            <div id="read_progress_bar" class="read_progress_bar"></div>
    </div>

    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        let docHeight = $("body").height();
        let windowHeight = $(window).height();

        $(window).scroll(function(){
            let scrollTop = $(this).scrollTop(); // 抓取當前scroll高度
            $(".read_progress_bar").css("width" ,`${Math.floor(100*scrollTop/(docHeight-windowHeight))}%`); // 計算當前scroll高度佔整體可視高度多少%
        
        })

    </script>
 </body>
```
