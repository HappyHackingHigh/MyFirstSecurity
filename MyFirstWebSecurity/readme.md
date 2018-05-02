# MyFirstWebSecurity(我的第一堂網站安全課)

>* 基礎入門課程
>* HappyHackingDay網站安全體驗營
>* 3小時課程為主(可動態調整2-4小時)

課程內容:本課程將帶領學生完成底下實測
>* HTTP協定的基礎實測與分析
>* 熟悉網站安全測試工具:developer Tools, Curl與Burpsuite
  (若有時間可示範OWASP Mantra或HackingBar)
>* 完成Web-CTF101的題目

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

```
### B.2.Curl::强大的http命令行工具

>* https://en.wikipedia.org/wiki/CURL
>* 使用 Curl::Curl command
```
https://www.tutorialspoint.com/unix_commands/curl.htm
```
>* 更多訊息  請參閱Everything curl https://ec.haxx.se/

### B.2.1.使用Curl測試HTTP協定[HTTP方法]==>解Web-CTF101/New Http Methond
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


### C.burp suite

### web-5:使用burp suite:HTTP封包攔截與竄改session


# 下一階段學習：Web hacking and exploitations

```
認識網站十大類型漏洞：OWASP TOP 10(2017)
https://www.owasp.org/index.php/Top_10-2017_Top_10
```

```
A1:2017-Injection
A2:2017-Broken Authentication

A3:2017-Sensitive Data Exposure

A4:2017-XML External Entities (XXE){新增}

A5:2017-Broken Access Control

A6:2017-Security Misconfiguration

A7:2017-Cross-Site Scripting (XSS)

A8:2017-Insecure DeserializationP{新增}
Insecure deserialization often leads to remote code execution.

A9:2017-Using Components with Known Vulnerabilities

A10:2017-Insufficient Logging&Monitoring{新增}
```

### D.先體驗一下：web-6:LFI
```
index.php?page=../../../../../../../../../flag
```

### A1:2017-Injection
```
單單Injection的各種面向就可以講兩天：
SQL injection(SQLi)
NoSQL injection
Command injection(cmdi) 
XPATH injection
LDAP injection

```
### A1-1.我的第一次SQL Injection

### A1-2.我的第一次Command Injection

# 想要學習更多,記得一定要報上｛網站安全研習營｝的課

## HTTP協定(2):HTTP Authentication認證{網站安全研習營再講}

