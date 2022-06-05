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
$("p").hover( function1 , function2 );  //第一個引數控制進入時的動作;第二個引數控制離開時的動作
```
