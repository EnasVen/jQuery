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


# CSS優先權
在JS內套用CSS的排序優先度如下:  
in-line > embedding/linking > out-sourcing  

而selector的CSS套用優先度如下:  
id > class > tag name  

# 
