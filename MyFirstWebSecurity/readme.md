# MyFirstWebSecurity(我的第一堂網站安全課)

>* 基礎入門課程
>* HappyHackingDay網站安全體驗營
>* 3小時課程為主(可動態調整2-4小時)

課程內容:本課程將帶領學生完成底下實測
>* HTTP協定的基礎實測與分析
>* 熟悉網站安全測試工具的使用:developer Tools, Curl與Burpsuite
>* 若有時間可示範OWASP Mantra或HackingBar
>* 完成Web-CTF101的題目

##### [上課演練平台:國網cdx-正式平台:](http://140.110.112.31)
##### [上課演練平台:其他平台:]

## Web-CTF101
```
請同學先登入網站註冊並實際看看Web-CTF101的題目
```

# A1:Developer Tools
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

### A1_1:使用{developer Tools開發者工具}來查看網站應用程式的原始碼Web-CTF101

### A1_2:使用{developer Tools開發者工具}來解HITCON2017的Visual Acuity

http://ctf2017.hitcon.org/

![result](pic/HITCON2017.png)

### A2:認識robots.txt
```
https://zh.wikipedia.org/wiki/Robots.txt
```

### A2_1:解Web-CTF101那題robots.txt

## B.1.HTTP協定(1): Http request and response

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


### B.2.Curl::强大的http命令行工具

>* https://en.wikipedia.org/wiki/CURL
>* 使用 Curl command
```
https://www.tutorialspoint.com/unix_commands/curl.htm
```
>* 更多訊息  請參閱Everything curl https://ec.haxx.se/

```
curl -X get -v http://120.114.62.89:3001/index.php
```
```
curl -X get -v http://120.114.62.89:3001/index.php
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

## Http request
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
## Http response
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

curl -X GETFLAG -v 'http://35.194.128.89:2004/index.php'

```
### web-4:使用Curl解Web-CTF101/flashing redirect


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
### web-5:使用burp suite:HTTP封包攔截與竄改session
```
你知道如何使用非管理者身分在設計不良的網站取得管理者權限登入嗎?
本題任務是請你完成上述使命?
提示1: 你知道如何攔截並修改封包嗎?
提示2: 你可以使用Burp Suite等工具

請連結以下網址進行解題:
http://140.110.112.31:2005/
```

使用Ubuntu 16.04預建的Mozilla/firefox

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




