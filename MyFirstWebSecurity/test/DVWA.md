# DVWA（Damn Vulnerable Web Application）

DVWA（Damn Vulnerable Web Application）是一個用來進行安全脆弱性鑒定的PHP/MySQL Web應用，
旨在為安全專業人員測試自己的專業技能和工具提供合法的環境，幫助web開發者更好的理解web應用安全防范的過程。

### [演練平台](http://120.114.102.164)

### [OWASP TOP 10漏洞OWASP Top 10 2017](https://www.owasp.org/index.php/Top_10-2017_Top_10)

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

# DVWA漏洞模組(尚未涵蓋2017年版TOP 10)

>* Command Injection（命令行注入）
>* SQL Injection（SQL注入）
>* SQL Injection（Blind）（SQL盲注）
>* Brute Force（暴力（破解））
>* Insecure CAPTCHA（不安全的驗證碼)
>* File Inclusion（文件包含）
>* File Upload（文件上傳）

>* XSS（Reflected）（反射型跨站腳本）
>* XSS（Stored）（存儲型跨站腳本）
>* XSS(DOM)
>* CSRF（跨站請求偽造）

DVWA 分為四種安全級別：Low，Medium，High，Impossible。

# Command Injection（命令行注入）

### Low

### Medium

### High

### Impossible


# SQL Injection（SQL注入）

### Low
```
步驟一:登錄DVWA

步驟二:選擇安全級別
將dvwa-security-裏面的安全級別調到最低級別

步驟三:選擇XSS(Reflected)題目頁面

步驟四:進行攻擊測試
輸入測試腳本<script>alert(\xss\)</script>點擊提交

==>成果畫面:瀏覽器會彈出“\xss\”
由於此處存在反射性XSS漏洞瀏覽器會彈出“\xss\”
```
關鍵程式碼解析
```
<?php 

if( isset( $_POST[ 'Submit' ]  ) ) { 
    // Get input 
    $target = $_REQUEST[ 'ip' ]; 

    // Determine OS and execute the ping command. 
    if( stristr( php_uname( 's' ), 'Windows NT' ) ) { 
        // Windows 
        $cmd = shell_exec( 'ping  ' . $target ); 
    } 
    else { 
        // *nix 
        $cmd = shell_exec( 'ping  -c 4 ' . $target ); 
    } 

    // Feedback for the end user 
    echo "<pre>{$cmd}</pre>"; 
} 

?> 


### Medium

### High

### Impossible

# SQL Injection（Blind）（SQL盲注）

### Low

### Medium

### High

### Impossible

# Brute Force（暴力（破解））

### Low

### Medium

### High

### Impossible

# Insecure CAPTCHA（不安全的驗證碼)

### Low

### Medium

### High

### Impossible

# File Inclusion（文件包含）
>* Local file Inclusion(LFI)
>* Remote file Inclusion(RFL)

### Low

### Medium

### High

### Impossible

# File Upload（文件上傳）

### Low

### Medium

### High

### Impossible

# XSS（Reflected）（反射型跨站腳本）

### Low
```
步驟一:登錄DVWA

步驟二:選擇安全級別
將dvwa-security-裏面的安全級別調到最低級別

步驟三:選擇XSS(Reflected)題目頁面

步驟四:進行攻擊測試
輸入測試腳本<script>alert(\xss\)</script>點擊提交

==>成果畫面:瀏覽器會彈出“\xss\”
由於此處存在反射性XSS漏洞瀏覽器會彈出“\xss\”
```
### Medium

### High

### Impossible

# XSS（Stored）（存儲型跨站腳本）。

### Low

### Medium

### High

### Impossible

# XSS(DOM)

### Low

### Medium

### High

### Impossible

# CSRF（跨站請求偽造）

### Low

### Medium

### High

### Impossible
