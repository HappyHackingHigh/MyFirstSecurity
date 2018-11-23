# JavaScript - Document對象內容集合
```
對象屬性
document.title //設置文檔標題等價於HTML的title標籤
document.bgColor //設置頁面背景色
document.fgColor //設置前景色(文本顏色)
document.linkColor //未點擊過的鏈接顏色
document.alinkColor //激活鏈接(焦點在此鏈接上)的顏色
document.vlinkColor //已點擊過的鏈接顏色
document.URL //設置URL屬性從而在同一窗口打開另一網頁
document.fileCreatedDate //文件建立日期，只讀屬性
document.fileModifiedDate //文件修改日期，只讀屬性
document.fileSize //文件大小，只讀屬性
document.cookie //設置和讀出cookie
document.charset //設置字符集 簡體中文:gb2312
———————————————————————
常用對象方法
document.write() //動態向頁面寫入內容
document.createElement(Tag) //創建一個html標籤對象
document.getElementById(ID) //獲得指定ID值的對象
document.getElementsByName(Name) //獲得指定Name值的對象
document.body.appendChild(oTag)
———————————————————————

body-主體子對象
document.body //指定文檔主體的開始和結束等價於body>/body>
document.body.bgColor //設置或獲取對象後面的背景顏色
document.body.link //未點擊過的鏈接顏色
document.body.alink //激活鏈接(焦點在此鏈接上)的顏色
document.body.vlink //已點擊過的鏈接顏色
document.body.text //文本色
document.body.innerText //設置body>…/body>之間的文本
document.body.innerHTML //設置body>…/body>之間的HTML代碼
document.body.topMargin //頁面上邊距
document.body.leftMargin //頁面左邊距
document.body.rightMargin //頁面右邊距
document.body.bottomMargin //頁面下邊距
document.body.background //背景圖片

document.body.appendChild(oTag) //動態生成一個HTML對象

常用對象事件
document.body.onclick=」func()」 //鼠標指針單擊對象是觸發
document.body.onmouseover=」func()」 //鼠標指針移到對象時觸發
document.body.onmouseout=」func()」 //鼠標指針移出對象時觸發
———————————————————————
location-位置子對象

document.location.hash // #號後的部分
document.location.host // 域名+端口號
document.location.hostname // 域名
document.location.href // 完整URL
document.location.pathname // 目錄部分
document.location.port // 端口號
document.location.protocol // 網絡協議(http:)
document.location.search // ?號後的部分

documeny.location.reload() //刷新網頁
document.location.reload(URL) //打開新的網頁
document.location.assign(URL) //打開新的網頁
document.location.replace(URL) //打開新的網頁
———————————————————————
selection-選區子對象
document.selection
———————————————————————

images集合(頁面中的圖像)

a)通過集合引用
document.images //對應頁面上的img標籤
document.images.length //對應頁面上img標籤的個數
document.images[0] //第1個img標籤
document.images[i] //第i-1個img標籤

b)通過nane屬性直接引用
img name=」oImage」
document.images.oImage //document.images.name屬性

c)引用圖片的src屬性
document.images.oImage.src //document.images.name屬性.src

d)創建一個圖像
var oImage
oImage = new Image()
document.images.oImage.src=」1.jpg」
同時在頁面上建立一個img /標籤與之對應就可以顯示

———————————————————————-

forms集合(頁面中的表單)

a)通過集合引用
document.forms //對應頁面上的form標籤
document.forms.length //對應頁面上/formform標籤的個數
document.forms[0] //第1個/formform標籤
document.forms[i] //第i-1個/formform標籤
document.forms[i].length //第i-1個/formform中的控件數
document.forms[i].elements[j] //第i-1個/formform中第j-1個控件

b)通過標籤name屬性直接引用
/formform name=」Myform」>input name=」myctrl」/>/form
document.Myform.myctrl //document.表單名.控件名

c)訪問表單的屬性
document.forms[i].name //對應form name>屬性
document.forms[i].action //對應/formform action>屬性
document.forms[i].encoding //對應/formform enctype>屬性
document.forms[i].target //對應/formform target>屬性

document.forms[i].appendChild(oTag) //動態插入一個控件
document.all.oDiv //引用圖層oDiv
document.all.oDiv.style.display=」" //圖層設置為可視
document.all.oDiv.style.display=」none」 //圖層設置為隱藏
document.getElementId(」oDiv」) //通過getElementId引用對象
document.getElementId(」oDiv」).style=」"
document.getElementId(」oDiv」).display=」none」
/*document.all表示document中所有對象的集合
只有ie支持此屬性，因此也用來判斷瀏覽器的種類*/

圖層對象的4個屬性
document.getElementById(」ID」).innerText //動態輸出文本
document.getElementById(」ID」).innerHTML //動態輸出HTML
document.getElementById(」ID」).outerText //同innerText
document.getElementById(」ID」).outerHTML //同innerHTML

資料來源 : http://www.ccvita.com/80.html
```
