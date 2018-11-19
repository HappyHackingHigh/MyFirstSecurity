```
JavaScript实战：JavaScript、jQuery、HTML5、Node.js实例大全
 出版社：	 清华大学出版社
https://pan.baidu.com/s/1Bp4FRpOERC9ghpjOPY2xHg
ha6w
```

### 2.1.1  最簡單表單的HTML結構
```
<!DOCTYPE html>
<html>
 <head>
  <title>最簡單表單的HTML結構</title>
 </head>
 <body>
	<form method="post" action="">
		帳戶：<input type="text" name="" /><br /><br />
		密碼：<input type="password" name="" /><br /><br />
		確認：<input type="password" name="" /><br /><br />
		<input type="submit" value="註冊"/>
	</form>
 </body>
</html>

```
### 2.1.2  綁定驗證功能
```
<!DOCTYPE html>
<html>
 <head>
  <title>最簡單表單的HTML結構</title>
 </head>
 <body>
	<form method="post" action="">
		帳戶：<input type="text" name="" id="userid" /><br /><br />
		密碼：<input type="password" name="" id="userpwd" /><br /><br />
		確認：<input type="password" name="" id="userpwd2" /><br /><br />
		<input type="submit" value="註冊" onclick="return eg.regCheck();" />
	</form>
	<script>
	var eg = {};//聲明一個物件，當做命名空間來使用，本書預設的範例都會以此來管理
		eg.regCheck = function(){
..................................
		}
	</script>
 </body>
</html>

```

```
<!DOCTYPE html>
<html>
 <head>
  <title>最簡單表單的HTML結構</title>
 </head>
 <body>
	<form method="post" action="">
		帳戶：<input type="text" name="" id="userid" /><br /><br />
		密碼：<input type="password" name="" id="userpwd" /><br /><br />
		確認：<input type="password" name="" id="userpwd2" /><br /><br />
		<input type="submit" value="註冊" onclick="return eg.regCheck();" />
	</form>
	<script>
		var eg = {};//聲明一個物件，當做命名空間來使用，本書預設的範例都會以此來方便管理
			//定義一個公共函數來獲取指定id元素的值，減少代碼量，提高代碼複用率
			eg.$ = function(id){
				return document.getElementById(id);
			};
			eg.regCheck = function(){
				var uid = eg.$("userid");
				var upwd = eg.$("userpwd");
				var upwd2 = eg.$("userpwd2");
				if(uid.value == ''){
					alert('帳戶不能為空!');
					return false;
				}
				if(upwd.value == ''){
					alert('密碼不能為空!');
					return false;
				}
				if(upwd.value != upwd2.value){
					alert('兩次密碼輸入不相同!');
					return false;
				}
				return true;
			};
	</script>
 </body>
</html>
```
### 5.2  固定列寬的簡單瀑布流實現    72


5.2.1  簡單的HTML結構    73
```
<!DOCTYPE html>
<html>
 <head>
  <title>簡單固定列寬瀑布流</title>
  <link rel="stylesheet" href="eg5.css" />
 </head>
 <body>
	<div class="main">
		<div class="col"><img src="1.jpg" alt="" /><p>[1.jpg]</p></div>
		<div class="col"><img src="2.jpg" alt="" /><p>[2.jpg]</p></div>
		<div class="col"><img src="3.jpg" alt="" /><p>[3.jpg]</p></div>
		<div class="col"><img src="4.jpg" alt="" /><p>[4.jpg]</p></div>
	</div>
	<script src="base.js"></script>
	<script src="eg5.js"></script>
	<script>
	eg.getColMin();//計算第一批資料的高度
var dl = eg.getDataList(5,35);//初始化一些資料
	eg.add(dl);//補充剩下的資料
	eg.scroll();//啟動捲軸監聽
	</script>
 </body>
</html>

```
5.3.2  用Masonry實現任意非固定列寬瀑布流

https://masonry.desandro.com/
```
<!DOCTYPE html>
<html>
<head>
<title>非固定列寬瀑布流</title>
<style>.box{margin:3px;}</style>
</head>
<body>
<div class="w1000">
	<div id="container">
		<div class="box"><img src="1x1a.jpg" /></div>
		<div class="box"><img src="1x1b.jpg" /></div>
		<div class="box"><img src="1x3.jpg" /></div>
		<div class="box"><img src="2x1b.jpg" /></div>
		<div class="box"><img src="1x1c.jpg" /></div>
		<div class="box"><img src="1x1d.jpg" /></div>
		<div class="box"><img src="2x1c.jpg" /></div>
		<div class="box"><img src="1x1e.jpg" /></div>
		<div class="box"><img src="1x1f.jpg" /></div>
		<div class="box"><img src="2x1d.jpg" /></div>
	</div>
</div>
</body>
</html>
<script src="masonry.pkgd.js"></script>
<script>
var $container = document.getElementById("container");
var msnry = new Masonry( $container, {
  columnWidth: 250,//每一列的寬度
  itemSelector: '.box'//子元素的選擇器，是class的值
});
</script>
<!-- <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
<script src="jquery.masonry.min.js"></script>
<script>
var $container = $('#container');
$container.imagesLoaded(function(){
  $container.masonry({
    itemSelector : '.box',
    columnWidth : 250
  });
});
</script> -->

```

5.4  延遲載入圖片
```
<!DOCTYPE html>
<html>
<head>
<title>懶載入</title>
<style>
div{float:left; min-width:150px; min-height:150px;}
</style>
</head>
<body>
<div><img src="loading.gif" lzay-src="1.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="2.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="3.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="4.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="5.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="6.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="7.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="8.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="9.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="10.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="11.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="12.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="13.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="14.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="15.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="16.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="17.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="18.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="19.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="20.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="21.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="22.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="23.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="24.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="25.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="26.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="27.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="28.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="29.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="30.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="31.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="32.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="33.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="34.jpg" alt=""></div>
<div><img src="loading.gif" lzay-src="35.jpg" alt=""></div>
</body>
</html>
<script src="base.js"></script>
<script src="eg5.js"></script>
<script>
eg.lazy();//判斷頁面打開時的第一屏是否有需要載入的圖
window.onscroll = function(){//onscroll,onload,onresize只能這樣添加
	eg.lazy();
}
</script>
```
