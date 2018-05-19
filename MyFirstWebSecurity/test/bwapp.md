# bWAPP（buggy web Application）

>* bWAPP是一個整合各種常見漏洞和最新漏洞的開源Web應用程式，
>* bWAPP目的是説明網路安全愛好者、開發人員和學生發現並防止網路漏洞。
>* bWAPP包含了超過100種漏洞，涵蓋了所有主要的已知Web漏洞，包括OWASP Top10安全風險，
>* bWAPP已經包含了OpenSSL和ShellShock漏洞。
>* https://sourceforge.net/projects/bwapp/
>* bWAPP 2.2版是以OWASP Top 10 2013為依據

### [演練平台](http://120.114.102.164)

### [OWASP TOP 10漏洞(OWASP Top 10 2017)](https://www.owasp.org/index.php/Top_10-2017_Top_10)

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
# 實戰bWAPP
```
步驟一:登錄bWAPP

帳號:/密碼:bee/bug

步驟二:選擇安全級別
將dvwa-security-裏面的安全級別調到最低級別

步驟三:選擇題目頁面
步驟四:進行攻擊測試
```

## A1 - Injection [2017_A1]
```
HTML Injection - Reflected (GET)
HTML Injection - Reflected (POST)
HTML Injection - Reflected (Current URL)
HTML Injection - Stored (Blog)
iFrame Injection
LDAP Injection (Search)
Mail Header Injection (SMTP)
OS Command Injection
OS Command Injection - Blind
PHP Code Injection
Server-Side Includes (SSI) Injection
SQL Injection (GET/Search)
SQL Injection (GET/Select)
SQL Injection (POST/Search)
SQL Injection (POST/Select)
SQL Injection (AJAX/JSON/jQuery)
SQL Injection (CAPTCHA)
SQL Injection (Login Form/Hero)
SQL Injection (Login Form/User)
SQL Injection (SQLite)
SQL Injection (Drupal)
SQL Injection - Stored (Blog)
SQL Injection - Stored (SQLite)
SQL Injection - Stored (User-Agent)
SQL Injection - Stored (XML)
SQL Injection - Blind - Boolean-Based
SQL Injection - Blind - Time-Based
SQL Injection - Blind (SQLite)
SQL Injection - Blind (Web Services/SOAP)
XML/XPath Injection (Login Form)
XML/XPath Injection (Search)
```


## A2 - Broken Auth. & Session Mgmt.[2017_A2] 
```
Broken Authentication - CAPTCHA Bypassing
Broken Authentication - Forgotten Function
Broken Authentication - Insecure Login Forms
Broken Authentication - Logout Management
Broken Authentication - Password Attacks
Broken Authentication - Weak Passwords
Session Management - Administrative Portals
Session Management - Cookies (HTTPOnly)
Session Management - Cookies (Secure)
Session Management - Session ID in URL
Session Management - Strong Sessions
```

## A3 - Cross-Site Scripting (XSS) [2017_A7]
```
Cross-Site Scripting - Reflected (GET)
Cross-Site Scripting - Reflected (POST)
Cross-Site Scripting - Reflected (JSON)
Cross-Site Scripting - Reflected (AJAX/JSON)
Cross-Site Scripting - Reflected (AJAX/XML)
Cross-Site Scripting - Reflected (Back Button)
Cross-Site Scripting - Reflected (Custom Header)
Cross-Site Scripting - Reflected (Eval)
Cross-Site Scripting - Reflected (HREF)
Cross-Site Scripting - Reflected (Login Form)
Cross-Site Scripting - Reflected (phpMyAdmin)
Cross-Site Scripting - Reflected (PHP_SELF)
Cross-Site Scripting - Reflected (Referer)
Cross-Site Scripting - Reflected (User-Agent)
Cross-Site Scripting - Stored (Blog)
Cross-Site Scripting - Stored (Change Secret)
Cross-Site Scripting - Stored (Cookies)
Cross-Site Scripting - Stored (SQLiteManager)
Cross-Site Scripting - Stored (User-Agent)
```

## A4 - Insecure Direct Object References 
```
Insecure DOR (Change Secret)
Insecure DOR (Reset Secret)
Insecure DOR (Order Tickets)
```

## A5 - Security Misconfiguration [2017_A6]
```
Arbitrary File Access (Samba)
Cross-Domain Policy File (Flash)
Cross-Origin Resource Sharing (AJAX)
Cross-Site Tracing (XST)
Denial-of-Service (Large Chunk Size)
Denial-of-Service (Slow HTTP DoS)
Denial-of-Service (SSL-Exhaustion)
Denial-of-Service (XML Bomb)
Insecure FTP Configuration
Insecure SNMP Configuration
Insecure WebDAV Configuration
Local Privilege Escalation (sendpage)
Local Privilege Escalation (udev)
Man-in-the-Middle Attack (HTTP)
Man-in-the-Middle Attack (SMTP)
Old/Backup & Unreferenced Files
Robots File
```


## A6 - Sensitive Data Exposure [2017_A3]
```
Base64 Encoding (Secret)
BEAST/CRIME/BREACH Attacks
Clear Text HTTP (Credentials)
Heartbleed Vulnerability
Host Header Attack (Reset Poisoning)
HTML5 Web Storage (Secret)
POODLE Vulnerability
SSL 2.0 Deprecated Protocol
Text Files (Accounts)
```

## A7 - Missing Functional Level Access Control 
```
Directory Traversal - Directories
Directory Traversal - Files
Host Header Attack (Cache Poisoning)
Host Header Attack (Reset Poisoning)
Local File Inclusion (SQLiteManager)
Remote & Local File Inclusion (RFI/LFI)
Restrict Device Access
Restrict Folder Access
Server Side Request Forgery (SSRF)
XML External Entity Attacks (XXE)
```

## A8 - Cross-Site Request Forgery (CSRF)[2017不在列入] 
```
Cross-Site Request Forgery (Change Password)
Cross-Site Request Forgery (Change Secret)
Cross-Site Request Forgery (Transfer Amount)
```

## A9 - Using Known Vulnerable Components  [2017_A1]
```
Buffer Overflow (Local)
Buffer Overflow (Remote)
Drupal SQL Injection (Drupageddon)
Heartbleed Vulnerability
PHP CGI Remote Code Execution
PHP Eval Function
phpMyAdmin BBCode Tag XSS
Shellshock Vulnerability (CGI)
SQLiteManager Local File Inclusion
SQLiteManager PHP Code Injection
SQLiteManager XSS
```

## A10 - Unvalidated Redirects & Forwards 
```
Unvalidated Redirects & Forwards (1)
Unvalidated Redirects & Forwards (2)
```

## Other bugs... 
```
ClickJacking (Movie Tickets)
Client-Side Validation (Password)
HTTP Parameter Pollution
HTTP Response Splitting
HTTP Verb Tampering
Information Disclosure - Favicon
Information Disclosure - Headers
Information Disclosure - PHP version
Information Disclosure - Robots File
Insecure iFrame (Login Form)	
Unrestricted File Upload
```
## Extras
```

```
