# JavaScript 程式語法

```
英文字母大小寫：JavaScript 會區分英文字母的大小寫。
空白字元：JavaScript 會自動忽略多餘的空白字元。
分號：JavaScript 並沒有規定每個敘述的結尾一定要加上分號 (;)，除非是要將兩個敘述寫在同一行，才要在第一個敘述的結尾加上分號以做區隔
換行：JavaScript 沒有規定換行的方式，但是為了提高可讀性，建議您將不同的敘述一一換行。 
註解：JavaScript 提供了兩種註解符號，其中 // 為單行註解，/* */ 為多行註解。
```
### JavaScript 的data type(資料型態)
```
JavaScript 的型別分為下列兩種類型：
基本型別 (primitive type)：包括數值 (number)、字串 (string)、布林  (boolean)。
物件型別 (object type)：包括陣列 (array)、函式 (function)、物件 (object)。
```

### string 資料型態
```
JavaScript 針對字串提供了string 型別，並規定字串的前後必須加上雙引號 (") 或單引號 (‘)，但兩者不可混用，例如 “ 生日”、’birthday‘。
```

### boolean  資料型態

```
只能表示true ( 真) 或false ( 偽) 兩種值
當我們要表示的資料只有對與錯、開與關、是與否等兩種選擇時，就可以使用boolean 型別。
```

### 變數 (variable) 
```
變數 (variable) 是在程式中宣告一個名稱 ( 識別字)
電腦會提供一個預留的記憶體空間給這個名稱，然後程式設計人員可以利用它來存放數值、字串、布林、陣列、物件等資料。

變數的命名規則:
1.第一個字元可以是英文字母或底線 (_)，其它字元可以是英文字母、阿拉伯數字、ISO-8859-1 字元、Unicode 字元、底線 (_) 或錢字符號 ($)
2.英文字母要區分大小寫。
3.Unicode 字元的格式為 \uNNNN，其中NNNN 是Unicode 字元的十六進位表示法。
4.不能使用JavaScript 關鍵字、內建函式的名稱、內建物件的名稱。

使用var 關鍵字來宣告變數


```
### 運算子
```
JavaScript 提供的運算子包括：
算術運算子：+、-、*、/、% 
遞增/ 遞減運算子：++、--
邏輯運算子：&& ( 邏輯AND)、|| ( 邏輯OR)、! ( 邏輯NOT)
比較運算子：!=、==、!==、===、>、<、>=、<= 
位元運算子：& ( 位元AND)、| ( 位元OR)、^ ( 位元XOR)、~ ( 位元NOT)、<< ( 向左移位)、>> ( 向右移位)、>>> ( 向右無號移位)
指派運算子：=、+=、-=、*=、/=、%=、&=、|=、^=、<<=、>>=、>>>=
條件運算子：? :
型別運算子：typeof
```

## JavaScript 的流程控制
```
分成下列兩種類型：
[1]判斷結構 (decision structure)：
if
switch
[2]迴圈結構 (loop structure)：
for
while
do
for...in
```

### switch
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>流程控制範例</title>
    <script language="javascript">
  var X = prompt("請輸入1-5的數字", "");
  switch(X)
  {
    case "1":    	//當使用者輸入1時
      alert("ONE");
      break;
    case "2":    	//當使用者輸入2時
      alert("TWO");
      break;
    case "3":    	//當使用者輸入3時
      alert("THREE");
      break;
    case "4":    	//當使用者輸入4時
      alert("FOUR");
      break;
    case "5":    	//當使用者輸入5時
      alert("FIVE");
      break;
    default:    	//當使用者輸入1-5以外的數字時
      alert("您輸入的數字超過範圍！");
      break;
  }
    </script>
  </head>
  <body>
  </body>
</html
```


### for
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>流程控制範例</title>
    <script language="javascript">
  var X = prompt("請輸入正整數", "");
  var Total = 0;
  for (var i = 1; i <= X; i++)
  {
    Total = Total + i;			//這行敘述也可以改寫為Total += i;
  }
  alert(Total);

    </script>
  </head>
  <body>
  </body>
</html>
```
### do-while
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>流程控制範例</title>
    <script language="javascript">
  do
  {
    Number = prompt("請輸入1-10的數字", "");
    if (Number > 6)        	//太大了繼續做答
    {
      alert("太大了！請重新輸入！");
    }
    else if (Number < 6)  		//太小了繼續做答
    {
      alert("太小了！請重新輸入！");
    }
  }while(Number != 6)
  alert("答對了！");
  </script>
  </head>
  <body>
  </body>
</html>
```
## 函式 (function)
```
函式 (function) 是將一段具有某種功能的敘述寫成獨立的程式單元，然後給予特定名稱，以提高程式的重覆使用性及可讀性。
```

### 使用者自訂函式

使用function關鍵字宣告函式

```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>函式範例</title>
    <script language="javascript">
      function Greeting()		//宣告函式
      {
        var UserName = prompt("請輸入您的大名", "");
        alert(UserName + "您好！歡迎光臨！");
      }
      Greeting();				//呼叫函式
    </script>
  </head>
  <body>
  </body>
</html>
```
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>函式範例</title>
    <script language="javascript">
      function Greeting()		//宣告函式
      {
        var UserName = prompt("請輸入您的大名", "");
        alert(UserName + "您好！歡迎光臨！");
      }      
    </script>
  </head>
  <body>
    <h1><a href="javascript:Greeting()">點取此處以顯示歡迎訊息</a></h1>
  </body>
</html>
```
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>函式範例</title>
    <script language="javascript">
      function Convert2F(DegreeC)	//宣告名稱為Convert2F、參數為DegreeC的函式
      {
        var DegreeF = DegreeC * 1.8 + 32;
        alert("攝氏" + DegreeC + "度可以轉換為華氏" + DegreeF + "度");
      }
      var Temperature = prompt("請輸入攝氏溫度", "");
      Convert2F(Temperature);		//呼叫函式時要將輸入的攝氏溫度當成參數傳入
    </script>
  </head>
  <body>
  </body>
</html>
```

```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>函式範例</title>
    <script language="javascript">
      function Convert2F(DegreeC)	//宣告名稱為Convert2F、參數為DegreeC的函式
      {
        var DegreeF = DegreeC * 1.8 + 32;
        alert("攝氏" + DegreeC + "度可以轉換為華氏" + DegreeF + "度");
      }
      var Temperature = prompt("請輸入攝氏溫度", "");
      Convert2F(Temperature);		//呼叫函式時要將輸入的攝氏溫度當成參數傳入
    </script>
  </head>
  <body>
  </body>
</html>

```

## Array
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>範例</title>
  </head>
  <body>
    <table border="1">
    <script language="javascript">
      var DrinkNames = new Array("卡布奇諾咖啡", "拿鐵咖啡", "血腥瑪莉", 
        "長島冰茶", "愛爾蘭咖啡", "藍色夏威夷", "英式水果冰茶");
      for(var i = 0; i < DrinkNames.length; i++)
      {
        document.write("<tr><td>飲料" + (i+1) + "</td>");
        document.write("<td>" + DrinkNames[i] + "</td></tr>");
      } 
    </script>
    </table>
  </body>
</html>
```

```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>範例</title>
  </head>
  <body>
    <table border="1">
    <script language="javascript">
      var Students = new Array(5);
      for(var i = 0; i < Students.length; i++)
        Students[i] = new Array(2);				//宣告Array物件的元素為另一個Array物件
      Students[0][0] = "小丸子";				//一一指派二維陣列的值
      Students[1][0] = "花輪";
      Students[2][0] = "小玉";
      Students[3][0] = "美環";
      Students[4][0] = "丸尾";
      Students[0][1] = 80;
      Students[1][1] = 95;
      Students[2][1] = 92;
      Students[3][1] = 88;
      Students[4][1] = 85;
      for(var i = 0; i < Students.length; i++)	//使用巢狀迴圈顯示二維陣列的值
      {
        document.write("<tr>");
        for(var j = 0; j < Students[i].length; j++)
          document.write("<td>" + Students[i][j] + "</td>");
        document.write("</tr>");
      }
    </script>
    </table>
  </body>
</html>
```
