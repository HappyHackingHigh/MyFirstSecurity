
```
http://www.w3.org/Style/CSS/current-work.en.html
```
### CSS 


### CSS 基本語法

### 7-2 CSS 樣式規則與選擇器
```
CSS 樣式表是由一條一條的樣式規則 (style rule) 所組成，
而樣式規則包含選擇器 (selector) 與宣告 (declaration) 兩個部分

h1 {color:red; font-family:"標楷體"}

選擇器 (selector)==> h1
宣告 (declaration)==>  {color:red; font-family:"標楷體"}
```
### 文字特效
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>CSS 樣式表練習1</title>
    <style type="text/css">
      h1 {color:red; font-family:"標楷體"}
      h2 {color:blue; font-family:"標楷體"}
    </style>
  </head>
  <body>
    <h1>素還真</h1>
     <h2>葉小釵</h2>   
  </body>
</html>
```
### 使用CSS 樣式表:四種方法

方法1:在 <head> 元素裡面嵌入樣式表
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>新網頁1</title>
	<style>
	  body {color:white; background:purple}
	</style>
  </head>
  <body>
    <h1>歡迎光臨！</h1>
  </body>
</html>	
```

方法2:使用HTML 元素的style 屬性指定樣式表
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>新網頁1</title>	
  </head>
  <body style="color:white; background:purple">
    <h1>歡迎光臨！</h1>
  </body>
</html>
```

方法3:將外部的樣式表匯入HTML 文件[推薦]

body.css
```
body {color:white; background:purple}
```

```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>新網頁1</title>
    <style>
      @import url("body.css");
    </style>	
  </head>
  <body>
    <h1>歡迎光臨！</h1>
  </body>
</html>
```
方法:將外部的樣式表連結至HTML 文件
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>新網頁1</title>
    <link rel="stylesheet" href="body.css" type="text/css">	
  </head>
  <body>
    <h1>歡迎光臨！</h1>
  </body>
</html>
```
### 使用類別選擇器定義樣式規則
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>唐詩欣賞</title>
	<style>
      .heading {font-family:華康粗黑體; font-size:30px ; color:maroon}
      .content {font-family:標楷體; font-size:25px; color:olive}
    </style>
  </head>
  <body> 
    <h1>唐詩欣賞</h1>  
    <p class="heading">春曉</p>
    <p class="content">春眠不覺曉，處處聞啼鳥。夜來風雨聲，花落知多少？</p>
    <p class="heading">竹里館</p>
    <p class="content">獨坐幽篁裡，彈琴復長嘯。深林人不知，明月來相照。</p> 
  </body>
</html>
```
### 使用ID 選擇器定義樣式規則
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>新網頁1</title>
	<style>
      #button1 {font-size:30px; color:red}
      #button2 {font-size:30px; color:green}      
    </style>
  </head>
  <body> 
    <h1>意見調查單</h1>
    <form>
      <input type="submit" value="提交" id="button1">
      <input type="reset" value="重新輸入" id="button2">
    </form>
  </body>
</html>
```

### 使用屬性選擇器定義樣式規則
```


```





CSS 提供了數個虛擬類別選擇器，如下：
連結虛擬類別 (link pseudo-classes)：包括 :link 和 :visited。
使用者動作虛擬類別 (user action pseudo-classes)：包括 :hover、:focus 和 :active。
語言虛擬類別 (language pseudo-class)：包括 :lang。
目標虛擬類別 (target pseudo-class)      ：包括 :target。
UI 元素狀態虛擬類別 (UI element states pseudo-classes)      ：包括 :enabled、:disabled、:checked、:indeterminate。
結構化虛擬類別 (structural pseudo-classes)       ：包括 :root、:nth-child()、:nth-last-child()、:nth-of-type()、:nth-last-of-type()、:ﬁrst-child、:last-child、:ﬁrst-of-type、:last-of-type、:only-child、:only-of-type、:empty。
否定虛擬類別 (negation pseudo-class)      ：包括 :not()
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>新網頁1</title>
	<style>
      input#button1 {font-size:30px; color:red}
      input#button2 {font-size:30px; color:green}      
    </style>
  </head>
  <body> 
    <h1 id="button1">意見調查單</h1>
    <form>
      <input type="submit" value="提交" id="button1">
      <input type="reset" value="重新輸入" id="button2">
    </form>
  </body>
</html>
```

```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>新網頁1</title>
	<style>
      #button1 {font-size:30px; color:red}
      #button2 {font-size:30px; color:green}      
    </style>
  </head>
  <body> 
    <h1 id="button1">意見調查單</h1>
    <form>
      <input type="submit" value="提交" id="button1">
      <input type="reset" value="重新輸入" id="button2">
    </form>
  </body>
</html>
```
### 圖片特效===2.9 圖片浮水印
```
<html>
 <head>
  <meta charset="UTF-8">
<style type="text/css">
div.shui{							/*浮水印*/
border:1px solid ;
opacity:0.5;						/*透明度設置*/
right:0;							/*浮水印居右*/
bottom:0;							/*浮水印居下*/
position:absolute;					/*一定要這樣設置*/
}
div.img{
border:1px solid ;					/*透明度設置*/
position:relative;					/*一定要這樣設置*/
display:inline-block;				/*div 寬度自我調整圖片寬度*/
}
img.big{							/*縮小一下圖片*/
width:250px;
height:150px;
}
</style>

</head>
<body>
<div class="img"><img src="4.jpg" class="big" /><div class="shui"><img src="google.jpg" /></div></div>
<div class="img"><img src="4.jpg" class="big" /><div class="shui">jianzhiunique原創作品</div></div>
</body>
</html>

```
### 圖片特效===2.14 幻燈片
```
<!doctype html>
<html lang="en">
 <head>
  <meta charset="UTF-8">
  <meta name="Generator" content="EditPlus®">
  <meta name="Author" content="">
  <meta name="Keywords" content="">
  <meta name="Description" content="">
  <title>幻燈片</title>
  <style type="text/css">
  *{margin:0;padding:0;list-style:none;}
  .powerpoint{
  position:absolute;
  width:100%; height:460px;
  background:black;
  overflow:hidden;
  }
  .powerpoint_big_pic>ul>li{
  position:absolute;top:0;left:-200px;/*  圖偏寬度大於螢幕寬度，大圖居中*/
  width:100%;height:100%;
  opacity:0;
  }
  .powerpoint_textlist{
  position:absolute;top:78%;left:10%;
  width:20%;height:15%;
  background:#7A7A7A;
  font-size:20px;
  color:#FFFFFF;
  }
  .powerpoint_textlist>ul>li{
  position:absolute;
  opacity:0;/*  文字的原理同大圖的原理*/
  }
  .powerpoint_small_pic{
  position:relative;top:78%;left:35%;
  width:51%;height:15%;
  background:#7A7A7A;
  overflow:hidden;
  }
  .powerpoint_small_pic>ul{
  position:relative;
  width:1500px;/*  設為大數以便li排成一排*/
  }
  .powerpoint_small_pic>ul>li{
  margin:5px;
  float:left;/*  左浮動*/
  }
  .powerpoint_pre,.powerpoint_next{
  position:absolute;top:81%;
  width:37px;height:38px;
  background:#303030;
  font-size:40px;
  color:#FFFFFF;
  border-radius:20px;
  cursor:pointer;
  }
  .powerpoint_pre{left:31%;}
  .powerpoint_next{left:87%;}
  </style>
  <script type="text/javascript" src="js/jq.js"></script>
  <script type="text/javascript">
  $(function(){
   var p=$(".powerpoint");//獲取整體，自動播放與暫停播放用到
   var pspu=$(".powerpoint_small_pic>ul");//獲取小圖ul
   var psp=$(".powerpoint_small_pic>ul>li");//獲取小圖li
   var  pbp=$(".powerpoint_big_pic>ul>li");//獲取大圖li
   var  ptl=$(".powerpoint_textlist>ul>li");//獲取文字說明li
   var  pre=$(".powerpoint_pre");//獲取上一個按鈕
   var  next=$(".powerpoint_next");//獲取下一個按鈕
   var now=0;//記錄當前被啟動元素的變數，作為參數傳入展示函數
   showpic(0);//頁面載入完成播放第一張
   var t=setInterval(function (){play()},4000);//自動播放
   p.hover(function (){clearInterval(t)},//滑鼠懸停清空計時器，暫停
				 function (){t=setInterval(function (){play()},4000)});//滑鼠移開繼續播放
   for (var i=0;i<psp.length ;i++ )//為每個小圖寫入點擊事件
   {
	   psp.eq(i).click(function (){
	   now=$(this).index();//將當前元素的索引存入變數
       showpic(now);
	   });
   }
   pre.click(function(){//前一個按鈕被點擊
	   if(0==now){
	   now=psp.length;//範圍限制
	   }
	   now=now-1;
	   showpic(now);
	   })
   next.click(function(){//前一個按鈕被點擊
	   if(psp.length-1==now){
	   now=-1;//範圍限制
	   }
	   now=now+1;
	   showpic(now);
	   })
	function play()//自動播放函數
	  {
		  showpic(now);
		  now++;
		  if(pbp.length==now)
		  {
			  now=0;
		  }
	  }
     function showpic(inow){//展示圖片函數
  	   for (var j=0;j<pbp.length ;j++ )//去除所有元素的可見性
	   {
		   pbp.eq(j).stop(true,false).animate({opacity:"0"},"normal");
		   ptl.eq(j).css("opacity","0");
		   psp.eq(j).css("border","0");
	   }
	   if(inow<6)//範圍限制
	   left=psp.eq(inow).offset().left-psp.eq(0).offset().left;//計算小圖示的左偏移值
	   else
	   left=psp.eq(6).offset().left-psp.eq(0).offset().left;//計算小圖示的左偏移值
	   pbp.eq(inow).stop(true,false).animate({opacity:"1"},"normal");//使編號為now元素可見
	   ptl.eq(inow).css("opacity","1");
	   psp.eq(inow).css("border","2px solid #FF7F00");
	   pspu.stop(true,false).animate({left:-left},"normal");//小圖滾動（left值改變）
  }
  });
  </script>
 </head>
 <body>
  <div class="powerpoint">
  <div class="powerpoint_big_pic">
   <ul>
   	<li><img src="img/b1.jpg" alt="" /></li>
   	<li><img src="img/b2.jpg" alt="" /></li>
   	<li><img src="img/b3.jpg" alt="" /></li>
   	<li><img src="img/b4.jpg" alt="" /></li>
   	<li><img src="img/b5.jpg" alt="" /></li>
   	<li><img src="img/b6.jpg" alt="" /></li>
   	<li><img src="img/b7.jpg" alt="" /></li>
   	<li><img src="img/b8.jpg" alt="" /></li>
	<li><img src="img/b9.jpg" alt="" /></li>
	<li><img src="img/b10.jpg" alt="" /></li>
	<li><img src="img/b11.jpg" alt="" /></li>
	<li><img src="img/b12.jpg" alt="" /></li>
	<li><img src="img/b13.jpg" alt="" /></li>
   </ul>
  </div>
  <div class="powerpoint_textlist">
  <ul>
  <li>《員警故事2013》 硬漢成龍演繹柔情父親</li>
  <li>《中國好歌曲》第四期 史上最美歌詞獲盛讚</li>
  <li>2014環球春晚 19：40直播 傑克遜經典重現</li>
  <li>2014新春觀劇指南 趙本山宋丹丹蔡明誰能打趴誰？</li>
  <li>天龍八部（至23集） 虛竹接任逍遙派掌門</li>
  <li>《與狼共舞2》主演做客 “特種兵”夫妻檔再續前緣</li>
  <li>《與狼共舞2》(至24集) 三人組陷四角戀</li>
  <li>《週末宅影院》 2013那些“雷瘋”的電影</li>
  <li>《中國達人秀》 終極考核戰虐心來襲</li>
  <li>《男媒婆》（至26集） 張庭女兒逼父母重婚</li>
  <li>《喋血孤島》（至30集） 紅葉被誣陷殺害芙蓉</li>
  <li>【英劇】神探默多克第七季 （至12集）塵封8年謀殺舊案終告破</li>
  <li>【美劇】軍旅軼事（至03集） 美國大兵展露純爺們兒氣質</li>
  </ul>
  </div>
  <div class="powerpoint_pre"><</div>
   <div class="powerpoint_small_pic">
   <ul>
   <li><img src="img/s1.jpg" alt="" /></li>
   <li><img src="img/s2.jpg" alt="" /></li>
   <li><img src="img/s3.jpg" alt="" /></li>
   <li><img src="img/s4.jpg" alt="" /></li>
   <li><img src="img/s5.jpg" alt="" /></li>
   <li><img src="img/s6.jpg" alt="" /></li>
   <li><img src="img/s7.jpg" alt="" /></li>
   <li><img src="img/s8.jpg" alt="" /></li>
   <li><img src="img/s9.jpg" alt="" /></li>
   <li><img src="img/s10.jpg" alt="" /></li>
   <li><img src="img/s11.jpg" alt="" /></li>
   <li><img src="img/s12.jpg" alt="" /></li>
   <li><img src="img/s13.jpg" alt="" /></li>
   </ul>
   </div>
   <div class="powerpoint_next">></div>
  </div>
 </body>
</html>

```

```

```

```

```
### CSS 3動畫特效
```
<!doctype html>
	<html lang="en">
	 <head>
	  <meta charset="UTF-8">
	  <meta name="Generator" content="EditPlus®">
	  <meta name="Author" content="">
	  <meta name="Keywords" content="">
	  <meta name="Description" content="">
	  <title>CSS 3動畫</title>
	  <style type="text/css">
	  div{
	  position:absolute;
	  animation:mymove 8s infinite;
	  -webkit-animation:mymove 8s infinite; /* Safari 和 Chrome */
	  height:50px;
	  width:100px;
	  top:300px;
	  border-radius:20px;
	  background:#3994C9;
	  text-align:center;
	  line-height:50px;
	  }
	  @keyframes mymove
	  {
	  0% {top:300px;left:0px;transform:rotate(50deg);}
	  20% {top:250px;left:450px;transform:rotate(80deg);height:100px;width:300px;} 
	  40% {top:300px;left:450px;transform:rotate(170deg);}
	  30% {top:300px;left:200px;transform:rotate(150deg);}
	  40% {top:300px;left:300px;transform:rotate(350deg);}
	  100% {top:300px;left:50px;transform:rotate(0deg);}
	  }
	  @-moz-keyframes mymove /* Firefox */
	  {
	  0% {top:300px;left:0px;-moz-transform:rotate(50deg);}
	  20% {top:250px;left:450px;-moz-transform:rotate(80deg);height:100px;width:300px;} 
	  40% {top:300px;left:450px;-moz-transform:rotate(170deg);}
	  30% {top:300px;left:200px;-moz-transform:rotate(150deg);}
	  40% {top:300px;left:300px;-moz-transform:rotate(350deg);}
	  100% {top:300px;left:50px;-moz-transform:rotate(0deg);}
	  }
	  @-webkit-keyframes mymove /* Safari 和 Chrome */
	  {
	  0% {top:300px;left:0px;-webkit-transform:rotate(50deg);}
	  20% {top:250px;left:450px;-webkit-transform:rotate(80deg);height:100px;width:300px;} 
	  40% {top:300px;left:450px;-webkit-transform:rotate(170deg);}
	  30% {top:300px;left:200px;-webkit-transform:rotate(150deg);}
	  40% {top:300px;left:300px;-webkit-transform:rotate(350deg);}
	  100% {top:300px;left:50px;-webkit-transform:rotate(0deg);}
	  }
	  @-o-keyframes mymove /* Opera */
	  {
	  0% {top:300px;left:0px;-o-transform:rotate(50deg);}
	  20% {top:250px;left:450px;-o-transform:rotate(80deg);height:100px;width:300px;} 
	  40% {top:300px;left:450px;-o-transform:rotate(170deg);}
	  30% {top:300px;left:200px;-o-transform:rotate(150deg);}
	  40% {top:300px;left:300px;-o-transform:rotate(350deg);}
	  100% {top:300px;left:50px;-o-transform:rotate(0deg);}
	  }
	  </style>
	

	 </head>
	 <body>
	  <div>-_-||</div>
	  <table border="1">
	  <tr>
	  	<td><b>屬性名稱</b></td>
	  	<td><b>屬性作用</b></td>
	  </tr>
	  <tr>
	  	<td>@keyframes</td>
	  	<td>定義一個動畫</td>
	  </tr>
	  <tr>
	  	<td>animation-name</td>
	  	<td>要應用到元素上的動畫的名稱</td>
	  </tr>
	  <tr>
	  	<td>animation-duration</td>
	  	<td>動畫完成一個過程的時間</td>
	  </tr>
	  <tr>
	  	<td>animation-timing-function</td>
	  	<td>動畫速度曲線，影響運動的類型。默認是 "ease"。</td>
	  </tr>
	  <tr>
	  	<td>animation-delay</td>
	  	<td>動畫開始的時間，即是否設置延遲</td>
	  </tr>
	  <tr>
	  	<td>animation-iteration-count</td>
	  	<td>動畫被播放的次數。默認是 1。</td>
	  </tr>
	  <tr>
	  	<td>animation-direction</td>
	  	<td>規定動畫是否在下一週期逆向地播放。默認是 "normal"。</td>
	  </tr>
	  <tr>
	  	<td>animation-play-state</td>
	  	<td>規定動畫的運行或暫停。默認是 "running"。</td>
	  </tr>
	  <tr>
	  	<td>animation-fill-mode</td>
	  	<td>規定物件動畫時間之外的狀態</td>
	  </tr>
	    <tr>
	  	<td>animation</td>
	  	<td>簡寫屬性，參數表列為上面除去@keyframes、animation-play-state、animation-fill-mode之外的所有屬性的值</td>
	  </tr>
	  </table>
	 </body>
	</html>

```

```

```

