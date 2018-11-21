
```
http://www.w3.org/Style/CSS/current-work.en.html
```

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
### 文字特效
```

```
### 2.9 圖片浮水印
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

```

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

