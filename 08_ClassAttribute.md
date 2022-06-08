# 新增/刪除/切換/判別元素類別
1. addClass("className")可以將selector內的元素增加指定類別
範例語法如下:
```
$("#div01").addClass("c1");
```

2. removeClass("className")可刪除元素內的指定類別
3. toggleClass("className")可將元素的類別切換至另一個
以下為經典的漢堡清單按鈕:
```
<head>
    <style>
        body{
            background: #ccc;
        }
        .transition{
            transition: 0.4s;
        }
        .wrapper{
            width:800px;
            margin: 20px auto;
        }
        .menu{
            display: inline-block;
            cursor: pointer;
            position: relative;
            padding: 0 0 0 2px;
            /* background:red; */
        }
        .menu.active{
            background: #fff;
            
        }
        .menu ul{
            position: relative;
            left:0;
            top:0;
            background:rgba(255,255,255,.8);
            width:120px;
            opacity: 0; /*表示完全透明 */
            max-height: 0;
            /* height: 500px; */
            overflow: hidden;
        }
        .menu.active ul{
            opacity: 1;
            max-height: 300px;
            /* height: 500px; */
        }
        .menu ul li a{
            display: block;
            padding:10px 12px;    
        }
        .menu ul li a:hover{
            background: lightblue;
        }
        ul,li{
            list-style: none;
            padding: 0;
            margin: 0;
        }
        .bar{
            width: 36px;
            height: 6px;
            background: #666;
            margin: 6px 0;
            border-radius: 2px;
        }
        .menu.active .bar1{
            transform: rotate(-45deg) translate(-9px, 7px) ;                 
        }
        
        .menu.active .bar2{opacity: 0;}
        
        .menu.active .bar3{
            transform: rotate(45deg) translate(-9px, -8px) ;      
        } 
        
    </style>          
</head>
<body>
    <div class="wrapper">
        <div class="menu transition" >
            <div class="bar bar1 transition"></div> //原始漢堡清單按鈕即為3個填色div所組成
            <div class="bar bar2 transition"></div>
            <div class="bar bar3 transition"></div>
            <ul class="transition">
                <li><a class="transition">Home</a></li>
                <li><a class="transition">Shop</a></li>
                <li><a class="transition">Gallery</a></li>
                <li><a class="transition">About</a></li>
            </ul>
        </div>
    </div>  
    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        $(".menu").click(function(){
            $(this).toggleClass("active"); // 透過toggle切換menu的class
        });
    </script>
</body>
```
4. hasClass("className")用來判斷selector是否具備特定class name，回傳true/false  

# CSS優先權
在JS內套用CSS的排序優先度如下:  
in-line > embedding/linking > out-sourcing  

而selector的CSS套用優先度如下:  
id > class > tag name  

# 滾動固定navigator導覽列
利用scroll事件來判定當可視高度>瀏覽器高度時(往下滾輪瀏覽網頁)，將導覽列安置在網頁最上方(position:fixed)，同時運用addClass與removeClass來達成:
```
<script>
    //offset() ：讀取指定元素在頁面(文件)上的相對坐標，
    //回傳含有top及left屬性的物件                  

    $(window).scroll(function(){
        let navPosition = $("#navbar").offset().top;
        console.log("navPosition="+navPosition);

        $(window).scroll(function(){
            let scrollTop = $(this).scrollTop();
            console.log(scrollTop);

            if(scrollTop>navPosition){
                $("#navbar").addClass("fixed_nav");
            }else{
                $("#navbar").removeClass("fixed_nav");
            }
        })
    });
</script>
```


# 切換頁面文字大小
首先，HTML5新增了一個功能讓使用者能夠自訂屬性，這些自訂屬性以data-開頭，例如: data-name , data-age ...etc。  
這些自訂屬性可以用.data("dash後面的名稱")的方式來呼叫，例如: $("h2").data("age");  

```
<head>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
    <style>
        .m{
            font-size: 1rem; //預先設定字型的CSS，之後直接改class就能套用
        }
        .s{
            font-size: 0.75rem;
        }
        .l{
            font-size: 1.25rem;
        }
        
    </style>
</head>
<body>
    <div class="container">
        <div class="py-2 d-flex justify-content-end">
            <div class="btn-group" role="group" aria-label="Basic example" id="change_btns">
                <button type="button" class="btn btn-secondary" data-size="s">小</button>
                <button type="button" class="btn btn-secondary" data-size="m">中</button>
                <button type="button" class="btn btn-secondary" data-size="l">大</button>
            </div>
        </div>
        <h2>NBA／聽到詹皇讚美自己 東契奇興奮直呼：他是我偶像</h2>
        <p>達拉斯獨行俠的「歐洲金童」Luka Doncic，前天出戰湖人，和「詹皇」LeBron James同場繳出至少30分「大三元」，表現相當精采，詹皇賽後也稱讚這名後輩， Doncic更直呼詹皇就是他的偶像。</p>
        <p>今天兩隊各自有比賽，不過話題依舊圍繞在前天的獨行俠、湖人之戰，當時湖人憑藉著詹皇39分12籃板16助攻，最終在延長賽擊敗獨行俠， Doncic則繳出31分15助攻13籃板，令人驚豔。</p>
        <p>詹皇今天受訪時再度被問到關於 Doncic的話題，他也不吝稱讚，給出高度評價，「顯然他是一個年輕且偉大的天才，我喜歡他的比賽，他不僅會替自己製造機會，也會幫助隊友。」</p>
        <p>而Doncic賽後被記者問到對於詹皇稱讚，他說，「這對我來說真的很瘋狂，我一直努力追隨著他，從一開始他就是我的偶像，能和他同場較勁，聽到他對我的讚美，對我來說很特別。」</p>
        
    </div>
    <script src="../js/jquery-3.6.0.min.js"></script>
    <script>
        // 按鈕置中
        $(".btn").eq(1).addClass("active");            
        $(".btn").click(function(){
            let size = $(this).data("size");
            console.log(size);
             $(this).addClass("active").siblings().removeClass('active');
            $("html").removeClass().addClass(size);           
        });
    </script>
</body>
```
