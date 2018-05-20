# MyFirstWebSecurity(我的第一堂網站安全課)

>* 基礎入門課程
>* HappyHackingDay網站安全體驗營
>* 3小時課程為主(可動態調整2-4小時)

課程內容:本課程將帶領學生完成底下實測
>* HTTP協定的基礎實測與分析
>* 熟悉網站安全測試工具的使用:developer Tools, Curl與Burpsuite
>* 若有時間可示範OWASP Mantra或HackingBar
>* 完成Web101-CTF的題目

##### [上課演練平台:國網cdx-正式平台:](http://140.110.112.31)
##### [上課演練平台:其他平台:]

## <<搶旗大賽實戰>> Web101-CTF
```
請同學先登入網站註冊並實際看看Web101-CTF的題目
```

# A1:Developer Tools[開發者工具:現代瀏覽器的強力駐軍]

```
https://developer.chrome.com/devtools

Chrome DevTools Masterclass
https://www.youtube.com/watch?v=KykP5Z5E4kA&t=2s

Debugging The Web (Chrome Dev Summit 2016)
https://www.youtube.com/watch?v=HF1luRD4Qmk

GoogleChrome/lighthouse
Auditing, performance metrics, and best practices for Progressive Web App
https://github.com/GoogleChrome/lighthouse
```

### <<搶旗大賽實戰>>Web101/Web-1:source code
***
使用{developer Tools開發者工具}來查看網站應用程式的原始碼

### <<搶旗大賽實戰>>HITCON ctf 2017/Visual Acuity
***
使用{developer Tools開發者工具}來解HITCON2017的Visual Acuity

http://ctf2017.hitcon.org/


## A2:認識robots.txt
```
https://zh.wikipedia.org/wiki/Robots.txt
```

### <<搶旗大賽實戰>>Web101/web-2:Robots.txt


# B.1.HTTP協定(1): Http request and response

```
Hypertext Transfer Protocol (HTTP) https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol

客戶端送出Http request給伺服器
client ====> Http request  =====> server

伺服器回應Http responses給客戶端
client <==== Http responses <===== server

資料傳送的狀態碼:HTTP status codes
https://en.wikipedia.org/wiki/List_of_HTTP_status_codes

Http request header fields的各個欄位
ttps://en.wikipedia.org/wiki/List_of_HTTP_header_fields#Request_fields

Response header fields的各個欄位
https://en.wikipedia.org/wiki/List_of_HTTP_header_fields#Response_fields
```

作業:查出Http request header fields的Authorization欄位,說明其意義

作業:查出Response header fields的WWW-Authenticate欄位,說明其意義


## B.2.Curl::强大的http命令行工具

>* https://en.wikipedia.org/wiki/CURL
>* [使用 Curl command](https://www.tutorialspoint.com/unix_commands/curl.htm)
>* 更多訊息  請參閱Everything curl https://ec.haxx.se/

作業:分析與說明curl -v www.google.com的執行畫面
```
* Rebuilt URL to: www.google.com/
*   Trying 172.217.160.100...
* Connected to www.google.com (172.217.160.100) port 80 (#0)
> GET / HTTP/1.1
> Host: www.google.com
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Date: Sun, 20 May 2018 08:36:32 GMT
< Expires: -1
< Cache-Control: private, max-age=0
< Content-Type: text/html; charset=ISO-8859-1
< P3P: CP="This is not a P3P policy! See g.co/p3phelp for more info."
< Server: gws
< X-XSS-Protection: 1; mode=block
< X-Frame-Options: SAMEORIGIN
< Set-Cookie: 1P_JAR=2018-05-20-08; expires=Tue, 19-Jun-2018 08:36:32 GMT; path=/; domain=.google.com
< Set-Cookie: NID=130=EccO9YHyMDYfaJyPrwGDogsHf-xRjCSS9D38sfkXyhsD7ceeUoZ5TlInN7nCJfBuloMT20KzcfKN-ARd0u1YLzATmvfxF1R1sDgwMPSz7GcbQf34aVW221xBpgKFnGd8; expires=Mon, 19-Nov-2018 08:36:32 GMT; path=/; domain=.google.com; HttpOnly
< Accept-Ranges: none
< Vary: Accept-Encoding
< Transfer-Encoding: chunked
< 
<!doctype html><html itemscope="" itemtype="http://schema.org/WebPage" lang="zh-TW"><head><meta content="text/html; charset=UTF-8" http-equiv="Content-Type">
................略...........................
```


範例:
```
curl -X get -v http://120.114.62.89:3001/index.php
```

執行畫面
```
Note: Unnecessary use of -X or --request, GET is already inferred.
*   Trying 120.114.62.89...
* Connected to 120.114.62.89 (120.114.62.89) port 3001 (#0)
> get /index.php HTTP/1.1
> Host: 120.114.62.89:3001
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 501 Not Implemented
< Date: Sat, 05 May 2018 05:39:42 GMT
< Server: Apache/2.4.7 (Ubuntu)
< X-Powered-By: PHP/5.5.9-1ubuntu4.22
< Content-Length: 199
< Connection: close
< Content-Type: text/html
< 
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>501 Not Implemented</title>
</head><body>
<h1>Not Implemented</h1>
<p>get to /index.php not supported.<br />
</p>
* Closing connection 0
```
說明 Http request HEADER
```
> get /index.php HTTP/1.1
> Host: 120.114.62.89:3001
> User-Agent: curl/7.47.0
> Accept: */*
```
```
get /index.php HTTP/1.1

get:Http的八種方法之一
HTTP/1.1:使用的HTTP版本
```
說明 Http response HEADER
```
< HTTP/1.1 501 Not Implemented
< Date: Sat, 05 May 2018 05:39:42 GMT
< Server: Apache/2.4.7 (Ubuntu)
< X-Powered-By: PHP/5.5.9-1ubuntu4.22
< Content-Length: 199
< Connection: close
< Content-Type: text/html
< 
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>501 Not Implemented</title>
</head><body>
<h1>Not Implemented</h1>
<p>get to /index.php not supported.<br />
</p>
* Closing connection 0
```

### <<搶旗大賽實戰>>Web101/web-3:Curl-1

step1:先用瀏覽器看看
```
==>被導向到http://120.114.62.89:2014/no_flag_is_here.php
```

step2:利用curl捕捉首頁

curl -v http://120.114.62.89:2014/
```

* Rebuilt URL to: http://120.114.62.89:2014/
*   Trying 120.114.62.89...
* Connected to 120.114.62.89 (120.114.62.89) port 2014 (#0)
> GET / HTTP/1.1
> Host: 120.114.62.89:2014
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Date: Sun, 20 May 2018 07:45:13 GMT
< Server: Apache/2.4.7 (Ubuntu)
< Last-Modified: Wed, 11 Oct 2017 13:25:23 GMT
< ETag: "797-55b455b1c36c0"
< Accept-Ranges: bytes
< Content-Length: 1943
< Vary: Accept-Encoding
< Content-Type: text/html
< 
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="">
    <meta name="author" content="">
    <title>BreakALLCTF</title>
    <link href="css/bootstrap.min.css" rel="stylesheet">
    <link href="css/heroic-features.css" rel="stylesheet">
</head>
<body>
    <nav class="navbar navbar-inverse navbar-fixed-top" role="navigation">
        <div class="container">
            <div class="navbar-header">
                <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1">
                    <span class="sr-only">Toggle navigation</span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                </button>
                <a class="navbar-brand" href="index.html">BreakALL CTF</a>
            </div>
        </div>
    </nav>
    <div class="container">
            <h2>BreakALL CTF</h2>
            </p>
        <hr>
        
        <div class="row">
            <div class="col-lg-12">
                <h4>你知道curl嗎?</h4>
            </div>
        </div>

        <div class="row text-center">

            <div class="col-sm-12 hero-feature">
                <div class="thumbnail">

                    <div class="caption">
                        <h3>flag在這!!!</h3>                
                        <p>
                            <a href="index.php" class="btn btn-primary">Go!</a>
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </div>
	
    <script src="js/jquery.js"></script>
    <script src="js/bootstrap.min.js"></script>
</body>

</html>
* Connection #0 to host 120.114.62.89 left intact
```
step3:仔細看看回傳的預設首頁==>找到關鍵index.php

step4:再次使用curl捕捉稍縱即逝的首頁
```
curl -v http://120.114.62.89:2014/index.php
```

```
*   Trying 120.114.62.89...
* Connected to 120.114.62.89 (120.114.62.89) port 2014 (#0)
> GET /index.php HTTP/1.1
> Host: 120.114.62.89:2014
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 302 Found
< Date: Sun, 20 May 2018 07:28:08 GMT
< Server: Apache/2.4.7 (Ubuntu)
< X-Powered-By: PHP/5.5.9-1ubuntu4.22
< Location: no_flag_is_here.php
< Content-Length: 34
< Content-Type: text/html
< 
BreakALLCTF{XXXXXXXXXXXXXXXXXXXXXXXXXXX}
* Connection #0 to host 120.114.62.89 left intact
```
### B.2.1.使用Curl測試HTTP協定[HTTP方法]==>解Web-CTF101/New Http Methond

>* HTTP方法(method):客戶端與伺服器溝通的方法(資料傳送的方法)
>* HTTP方法(method):https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html

>* 根據HTTP標準，HTTP請求可以使用多種請求方法。
>* HTTP1.0定義了三種請求方法： GET, POST 和 HEAD方法。
>* HTTP1.1新增了五種請求方法：OPTIONS, PUT, DELETE, TRACE 和 CONNECT 方法。

```
curl -X GET -v 'http://35.194.128.89:2004/index.php'
curl -X POST -v 'http://35.194.128.89:2004/index.php'
curl -X OPTIONS -v 'http://35.194.128.89:2004/index.php'
```
# <<搶旗大賽實戰>>Web101/web-4:HTTP method 100

curl -X GET -v http://140.110.112.31:3001/index.php

curl -v http://140.110.112.31:3001/index.php
```
*   Trying 140.110.112.31...
* Connected to 140.110.112.31 (140.110.112.31) port 3001 (#0)
> GET /index.php HTTP/1.1
> Host: 140.110.112.31:3001
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 501 Not Implemented
< Date: Sun, 20 May 2018 07:17:50 GMT
< Server: Apache/2.4.7 (Ubuntu)
< X-Powered-By: PHP/5.5.9-1ubuntu4.22
< Content-Length: 199
< Connection: close
< Content-Type: text/html
< 
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>501 Not Implemented</title>
</head><body>
<h1>Not Implemented</h1>
<p>GET to /index.php not supported.<br />
</p>
* Closing connection 0
</body></html>
```

curl -X POST -v http://140.110.112.31:3001/index.php
```
*   Trying 140.110.112.31...
* Connected to 140.110.112.31 (140.110.112.31) port 3001 (#0)
> POST /index.php HTTP/1.1
> Host: 140.110.112.31:3001
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 501 Not Implemented
< Date: Sun, 20 May 2018 07:18:07 GMT
< Server: Apache/2.4.7 (Ubuntu)
< X-Powered-By: PHP/5.5.9-1ubuntu4.22
< Content-Length: 200
< Connection: close
< Content-Type: text/html
< 
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>501 Not Implemented</title>
</head><body>
<h1>Not Implemented</h1>
<p>POST to /index.php not supported.<br />
</p>
* Closing connection 0
```

curl -X OPTIONS  -v http://140.110.112.31:3001/index.php
```
*   Trying 140.110.112.31...
* Connected to 140.110.112.31 (140.110.112.31) port 3001 (#0)
> OPTIONS /index.php HTTP/1.1
> Host: 140.110.112.31:3001
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Date: Sun, 20 May 2018 07:18:40 GMT
< Server: Apache/2.4.7 (Ubuntu)
< X-Powered-By: PHP/5.5.9-1ubuntu4.22
< Allow: GETFLAG,OPTIONS
< Content-Length: 0
< Content-Type: text/html
< 
* Connection #0 to host 140.110.112.31 left intact

```
curl -X GETFLAG  -v http://140.110.112.31:3001/index.php

```
*   Trying 140.110.112.31...
* Connected to 140.110.112.31 (140.110.112.31) port 3001 (#0)
> GETFLAG /index.php HTTP/1.1
> Host: 140.110.112.31:3001
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Date: Sun, 20 May 2018 07:19:34 GMT
< Server: Apache/2.4.7 (Ubuntu)
< X-Powered-By: PHP/5.5.9-1ubuntu4.22
< Content-Length: 33
< Content-Type: text/html
< 
* Connection #0 to host 140.110.112.31 left intact
BreakALLCTF{***********************}
```

## C.web debugging proxy之burp suite(ZAP,fiddler)

>* https://en.wikipedia.org/wiki/Burp_suite
>* kali linux 2018.1已經安裝burp suite free edition
>* Ubuntu linux 16.04 LTS 64-bit預設沒有安裝==>需自行安裝
>* https://portswigger.net/burp/communitydownload
```
下載burpsuite_community_linux_v1_7_33.sh

chmod +x burpsuite_community_linux_v1_7_33.sh

執行安裝==> ./burpsuite_community_linux_v1_7_33.sh
```

>* 設定瀏覽器==>使用Ubuntu 16.04預建的Mozilla/firefox
>* 參看圖片的設定畫面
```
Connection settings to use a proxy can be set in Firefox Preferences as follows:

    Click the menu button and choose Preferences. about:preferences ==>
    In the General panel, go to the Network Proxy section.
    Click Settings…. The Connection Settings dialog will open.

>* No proxy: Choose this if you don't want to use a proxy.
>* Auto-detect proxy settings for this network: Choose this if you want Firefox to automatically detect the proxy settings for your network.
>* Use system proxy settings: Choose this if you want to use the proxy settings configured for your operating system.
>* Manual proxy configuration: Choose this if you have a list of one or more proxy servers. Ask your system administrator for the configuration information. Each proxy requires a hostname and a port number.
        If the same proxy name and port number are used for all protocols, check Use this proxy server for all protocols.
>* No Proxy For: List of hostnames or IP addresses that will not be proxied. Use <local> to bypass proxying for all hostnames which do not contain periods. 
>* Automatic proxy configuration URL: Choose this if you have a proxy configuration (.pac) file. Enter the URL and click okay to save changes and load the proxy configuration.
>* Reload: The reload button will load the currently available proxy configuration. 
```

### <<搶旗大賽實戰>>Web101/Web-6:Burp Suite

web-:使用burp suite:HTTP封包攔截與竄改session
```
你知道如何使用非管理者身分在設計不良的網站取得管理者權限登入嗎?
本題任務是請你完成上述使命?
提示1: 你知道如何攔截並修改封包嗎?
提示2: 你可以使用Burp Suite等工具

請連結以下網址進行解題:
http://140.110.112.31:2005/
```
設定好攔截準備

Step1:先使用任意帳密登入並觀察瀏覽器畫面  test/123456

Step2:(使用Burpsuite攔截)再次使用任意帳密登入並觀察瀏覽器畫面  test/123456

仔細觀察header的欄位及送出的資料

Step3:(使用Burpsuite攔截)再次使用任意帳密登入 test/123456

Step4:修改Burpsuite攔截的封包:將guest 改成admin

Step5:forward(送出)修改過的封包並觀察瀏覽器畫面 ==>你就會看到答案

