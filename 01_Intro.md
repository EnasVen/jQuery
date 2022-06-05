# Pros & Cons
jQuery具備以下優點
1. 輕量級的JS library (write less , do more為其宗旨)
2. 簡化routine JS framework，方便存取或修改網頁部分內容
3. 支援AJAX功能、原生CSS語法並加入動畫效果
4. 解決JS無法相容於多種瀏覽器的問題
5. 提供Extension機制，方便撰寫plug-in功能

當然，也具備一些缺點 
1. jQuery無法支援JS的addEventListener寫法，也就是說無法實作event bubbling true的事件氣泡。
2. jQuery精簡版主程式不支援AJAX與其effects

# Downloads
透過官網 https://jquery.com 可下載jQuery主程式到local端，其分為2種版本:
1. 標準版(v1,v2,v3)
  - Uncompressed，即正常版，做為開發和除錯用，可讀性高  
  - Minified，即壓縮板，由正常版去掉註解、換行符號、空白、tab...etc，主要用於部署上線用  
2. 精簡版(v3)
  - Uncompressed，檔名結尾為slim.js  
  - Minified，檔名結尾為slim.min.js  


執行的語法(寫在JS script之前就必須載入):
```
<script src="../js/jquery-3.6.0.min.js"></script>
```

# online jQuery
另一種使用jQuery主程式的方法是透過掛載的方式執行，即CDN(Content Delivery Network or Content Distribution Network)  
這是一種以網路戶相連接的電腦網路系統，利用最靠近每位使用者的伺服器來傳遞內容。  
常用的CDN: jQueryCDN , GoogleCDN , MicrosoftCDN 以及 javaScript jQuery Deliver  
使用語法(寫在JS script之前就必須載入): 
```
<script src="https://code.jquery.com/jquery-3.6.0.js"
        integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
```
標籤內的integrity屬性即為驗證碼!  

# Start jQuery
在DOM tree建立後即可啟動jQuery處理程序，其意義類似JS內的DOMContentLoaded方法，寫法如下:  
```
<script>
    // //ready是一個事件，等到DOMTree產生後會執行這個事件
    // jQuery(document).ready(function () {
    //     console.log($("h1"));
    //     $("h1").css("color", "blue");
    // })

    // 精簡寫法
    $(function(){
        console.log($("h1"));
        $("h1").css("color", "orange");
    })
</script>
```

# Basic Syntax 
jQuery目的為簡化JS和HTML之間的操作。  
基本語法使用$關鍵字做為jQuery Libaray:
```
// 下面兩種方式同義
jQuery("selector").action();
$("selector").action();
```
和JS相同，使用分號代表一個敘述的結束。  
在selector選取網頁物件後，呼叫action進行後續修改  
讀取或設定CSS樣式語法為:
```
// 必須以字串符號呈現
$("selector").css("attr","value");
```

# Chain Syntax
經過jQuery selector $ 回傳的結果如果仍為jQuery selector，那麼可再次套用 action()進行後續動作。  
和JS相同，$(this)回傳的是正在處理的selector，而非HTML元素!   
透過$(this)回傳的結果為jQuery selector，類陣列;而在JS內，透過this回傳的是HTML物件，兩者有很大的不同!  
語法:
```
<script>
    $(document).ready(function () {
        // 寫法1 - origin
        $("h1").css("color", "green");
        $("h1").mouseover(function () {
            $(this).css("color", "red");
        });
        $("h1").mouseout(function () {
            $(this).css("color", "green");
        });

        // 寫法2 - chain 
        $("h1").css("color", "green").mouseover(function () {
            $(this).css("color", "red");
        }).mouseout(function () {
            $(this).css("color", "green");
        });

        // 寫法3 - 函數宣告
        function over() {
            $(this).css("color", "red");
            console.log(this);
        }

        function out() {
            $(this).css("color", "green");
        }
        $("h1").css("color", "green").mouseover(over).mouseout(out);
    });
</script>
```

chain常見錯誤: 
```
$(this).css("attr","value"); //回傳jQuery selector
$(this).css("attr"); //回傳css attr設定值，為字串
```
因此，欲套用jQuery chain action，回傳結果就必須是jQuery selector!!  

詳細語法可觀看W3School API介紹:  https://www.w3schools.com/jquery/default.asp
