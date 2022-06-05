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


