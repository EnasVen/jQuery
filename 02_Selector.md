# Selector
用來選取網頁內的元素，以陣列的型態封裝成jQuery物件回傳。  
jQuery主要分為以下2種:
1. CSS選擇器
  - 套用原生CSS selector語法產生的jQuery選擇器
2. jQuery自訂選擇器
  - 參考 [https://api.jquery.com/category/seletors/](https://api.jquery.com/category/selectors/)  
  - 須注意標籤內若包含 Selectors > jQuery Extensions則代表這種選擇器是jQuery獨有的寫法!  


# Basic Selector
基礎選擇器為CSS語法衍生:
> \* : ```$("*")``` 選取所有元素  
> element : ```$("div")``` 選取所有指定tag name元素  
> .class : ```$(".myClass")``` 選取所有指定class name元素  
> \#id : ```$("#myDiv")``` 選取所有指定id元素  
> [tag,id].class : ```$("div.a1")``` 複合型選取方式　　

# Form Selector
以 : 進行type選取  
> $(":button") : 選取type為butto以及標籤是button的元素  
> $(":checkbox") :  選取type為checkbox的所有元素  
> $(":checked") : 選取屬性為checked(被勾選)的所有元素，注意除了input標籤之外，select標籤內的option selected也算!  
> $(":selected") : 選取屬性為selected的所有元素，只計算selected底下有選擇的options
> $(":disabled") : 選取屬性為disable的所有元素  
> $(":enable") : 選取屬性為enable的所有元素  
> $(":file") : 選取type為file的所有元素  
> $(":image") : 選取type為image的所有元素  
> $(":input") : 選取表單中的所有元素  
> $(":password") : 選取type為password的所有元素  
> $(":radio") : 選取type為radio的所有元素  
> $(":reset") : 選取type為reset的所有元素  
> $(":submit") : 選取type為submit的所有元素  
> $(":text") :  選取type為text的所有元素  


# Attribute Selector
透過屬性名稱與屬性值來做選取:  
> $("tag[attr]") : 選擇有attr屬性的任何tagt元素  
> $("tag[attr=value]") : 選擇attr屬性值為value的所有tag元素  
> $("tag[attr!=value]") : 選擇attr屬性值不為value的所有tag元素 
> $("tag[attr^=value]") : 選擇attr屬性值開頭為value的所有tag元素 
> $("tag[attr*=value]") : 選擇attr屬性值內包含value的所有tag元素 
> $("tag[attr$=value]") : 選擇attr屬性值以value結尾的所有tag元素 
> $("tag[attr|=value]") : 選擇attr屬性值為value或value-的所有tag元素
> $("tag[attr1][attr2$=value]") : 複合是寫法，選擇attr1屬性值內，所有attr2屬性值為value的所有tag元素

 
# Hierarchy Selector

# Child Filter

# contant Filter

# Basic Filter

