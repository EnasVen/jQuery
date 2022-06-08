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

