# DVWA（Damn Vulnerable Web Application）

DVWA（Damn Vulnerable Web Application）是一個用來進行安全脆弱性鑒定的PHP/MySQL Web應用，
旨在為安全專業人員測試自己的專業技能和工具提供合法的環境，幫助web開發者更好的理解web應用安全防范的過程。

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

# DVWA漏洞模組(未涵蓋2017年版TOP 10)

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

DVWA 分為四種安全級別：Low，Medium，High，Impossible

# DVWA 測試步驟
```
步驟一:登錄DVWA

步驟二:選擇安全級別
將dvwa-security-裏面的安全級別調到最低級別

步驟三:選擇題目頁面

步驟四:進行攻擊測試
```

# Command Injection（命令行注入）

### Low
```
攻擊測試

step 1: 輸入127.0.0.1 ==> 點擊提交
step 2: 輸入127.0.0.1 ; cat /etc/passwd ==> 點擊提交
step 3: 輸入127.0.0.1 ; cat /etc/passwd | tee /tmp/passwd ==> 點擊提交

==>成果畫面

```
關鍵程式碼解析


```
<?php 

if( isset( $_POST[ 'Submit' ]  ) ) { 
    // 使用$_REQUEST來接收輸入的IP(完全沒有驗證使用者輸入的資料) 
    $target = $_REQUEST[ 'ip' ]; 

    // 決定作業系統並執行相對應的ping指令 OS and execute the ping command. 
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
```
>* PHP 預先定義的變數(Predefined Variables)$_REQUEST

### Medium

### High

### Impossible


# SQL Injection（SQL注入）

### Low


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

>* Authentication認證機制:通過一定的手段，完成對使用者身分的確認
>* 網站的存取權限(登入權限)基本都會以帳號與密碼為認證機制
>* 除此之外還有其他補強機制如CAPTCHA 圖形驗證碼
>* CAPTCHA==Completely Automated Public Turing Test to Tell Computers and Humans Apart

>* 多重要素(因子)驗證[Multi-factor authentication;MFA]
>* 雙重認證[Two-factor authentication;2FA]{雙重驗證|雙因素認證|二元認證}
>* 兩步驟驗證[2-Step Verification]{兩步驗證}
>* 使用兩種不同的元素，合併在一起，來確認使用者的身份，是多因素驗證中的一個特例。
>* 雙重認證範例:{銀行卡+ PIN碼}:使用銀行卡時，需要另外輸入PIN碼，確認之後才能使用其轉帳功能。

>* 測試環境說明:
### Low


一般測試步驟::<span style="color:blue">輸入驗證碼才可修改密碼</span>

```
攻擊測試步驟::使用burpsuite攔截封包將step=1修改為step=2,即可略過CAPTCHA驗證
```
關鍵程式碼分析

客戶端(使用者端)程式分析
```
................


	<div class="vulnerable_code_area">
		<form action="#" method="POST" >
			<h3>Change your password:</h3>
			<br />

			<input type="hidden" name="step" value="1" />
			New password:<br />
			<input type="password" AUTOCOMPLETE="off" name="password_new"><br />
			Confirm new password:<br />
			<input type="password" AUTOCOMPLETE="off" name="password_conf"><br />

			
		<script src='https://www.google.com/recaptcha/api.js'></script>
		<br /> <div class='g-recaptcha' data-theme='dark' data-sitekey='6Ldg-VcUAAAAAEHnHni9V92-gquni6bFKSHJ5YQM'></div>
	
			<br />

			<input type="submit" value="Change" name="Change">
		</form>
		<pre><br />The CAPTCHA was incorrect. Please try again.</pre>
	</div>
 
 ................
```
伺服器端程式分析
```
<?php 

if( isset( $_POST[ 'Change' ] ) && ( $_POST[ 'step' ] == '1' ) ) { 
    // Hide the CAPTCHA form 
    $hide_form = true; 

    // Get input 
    $pass_new  = $_POST[ 'password_new' ]; 
    $pass_conf = $_POST[ 'password_conf' ]; 

    // Check CAPTCHA from 3rd party 
    $resp = recaptcha_check_answer( 
        $_DVWA[ 'recaptcha_private_key'], 
        $_POST['g-recaptcha-response'] 
    ); 

    // Did the CAPTCHA fail? 
    if( !$resp ) { 
        // What happens when the CAPTCHA was entered incorrectly 
        $html     .= "<pre><br />The CAPTCHA was incorrect. Please try again.</pre>"; 
        $hide_form = false; 
        return; 
    } 
    else { 
        // CAPTCHA was correct. Do both new passwords match? 
        if( $pass_new == $pass_conf ) { 
            // Show next stage for the user 
            echo " 
                <pre><br />You passed the CAPTCHA! Click the button to confirm your changes.<br /></pre> 
                <form action=\"#\" method=\"POST\"> 
                    <input type=\"hidden\" name=\"step\" value=\"2\" /> 
                    <input type=\"hidden\" name=\"password_new\" value=\"{$pass_new}\" /> 
                    <input type=\"hidden\" name=\"password_conf\" value=\"{$pass_conf}\" /> 
                    <input type=\"submit\" name=\"Change\" value=\"Change\" /> 
                </form>"; 
        } 
        else { 
            // Both new passwords do not match. 
            $html     .= "<pre>Both passwords must match.</pre>"; 
            $hide_form = false; 
        } 
    } 
} 

if( isset( $_POST[ 'Change' ] ) && ( $_POST[ 'step' ] == '2' ) ) { 
    // Hide the CAPTCHA form 
    $hide_form = true; 

    // Get input 
    $pass_new  = $_POST[ 'password_new' ]; 
    $pass_conf = $_POST[ 'password_conf' ]; 

    // Check to see if both password match 
    if( $pass_new == $pass_conf ) { 
        // They do! 
        $pass_new = ((isset($GLOBALS["___mysqli_ston"]) && is_object($GLOBALS["___mysqli_ston"])) ? mysqli_real_escape_string($GLOBALS["___mysqli_ston"],  $pass_new ) : ((trigger_error("[MySQLConverterToo] Fix the mysql_escape_string() call! This code does not work.", E_USER_ERROR)) ? "" : "")); 
        $pass_new = md5( $pass_new ); 

        // Update database 
        $insert = "UPDATE `users` SET password = '$pass_new' WHERE user = '" . dvwaCurrentUser() . "';"; 
        $result = mysqli_query($GLOBALS["___mysqli_ston"],  $insert ) or die( '<pre>' . ((is_object($GLOBALS["___mysqli_ston"])) ? mysqli_error($GLOBALS["___mysqli_ston"]) : (($___mysqli_res = mysqli_connect_error()) ? $___mysqli_res : false)) . '</pre>' );

        // Feedback for the end user 
        echo "<pre>Password Changed.</pre>"; 
    } 
    else { 
        // Issue with the passwords matching 
        echo "<pre>Passwords did not match.</pre>"; 
        $hide_form = false; 
    } 

    ((is_null($___mysqli_res = mysqli_close($GLOBALS["___mysqli_ston"]))) ? false : $___mysqli_res); 
} 

?> 
```
### Medium
```
攻擊測試步驟::
使用burpsuite攔截封包並修改封包
將step=1修改為step=2,再增加&passed_captcha=true,即可略過CAPTCHA驗證
```
關鍵程式碼分析
``` 
<?php 

if( isset( $_POST[ 'Change' ] ) && ( $_POST[ 'step' ] == '1' ) ) { 
    // Hide the CAPTCHA form 
    $hide_form = true; 

    // Get input 
    $pass_new  = $_POST[ 'password_new' ]; 
    $pass_conf = $_POST[ 'password_conf' ]; 

    // Check CAPTCHA from 3rd party 
    $resp = recaptcha_check_answer( 
        $_DVWA[ 'recaptcha_private_key' ], 
        $_POST['g-recaptcha-response'] 
    ); 

    // Did the CAPTCHA fail? 
    if( !$resp ) { 
        // What happens when the CAPTCHA was entered incorrectly 
        $html     .= "<pre><br />The CAPTCHA was incorrect. Please try again.</pre>"; 
        $hide_form = false; 
        return; 
    } 
    else { 
        // CAPTCHA was correct. Do both new passwords match? 
        if( $pass_new == $pass_conf ) { 
            // Show next stage for the user 
            echo " 
                <pre><br />You passed the CAPTCHA! Click the button to confirm your changes.<br /></pre> 
                <form action=\"#\" method=\"POST\"> 
                    <input type=\"hidden\" name=\"step\" value=\"2\" /> 
                    <input type=\"hidden\" name=\"password_new\" value=\"{$pass_new}\" /> 
                    <input type=\"hidden\" name=\"password_conf\" value=\"{$pass_conf}\" /> 
                    <input type=\"hidden\" name=\"passed_captcha\" value=\"true\" /> 
                    <input type=\"submit\" name=\"Change\" value=\"Change\" /> 
                </form>"; 
        } 
        else { 
            // Both new passwords do not match. 
            $html     .= "<pre>Both passwords must match.</pre>"; 
            $hide_form = false; 
        } 
    } 
} 

if( isset( $_POST[ 'Change' ] ) && ( $_POST[ 'step' ] == '2' ) ) { 
    // Hide the CAPTCHA form 
    $hide_form = true; 

    // Get input 
    $pass_new  = $_POST[ 'password_new' ]; 
    $pass_conf = $_POST[ 'password_conf' ]; 

    // Check to see if they did stage 1 
    if( !$_POST[ 'passed_captcha' ] ) { 
        $html     .= "<pre><br />You have not passed the CAPTCHA.</pre>"; 
        $hide_form = false; 
        return; 
    } 

    // Check to see if both password match 
    if( $pass_new == $pass_conf ) { 
        // They do! 
        $pass_new = ((isset($GLOBALS["___mysqli_ston"]) && is_object($GLOBALS["___mysqli_ston"])) ? mysqli_real_escape_string($GLOBALS["___mysqli_ston"],  $pass_new ) : ((trigger_error("[MySQLConverterToo] Fix the mysql_escape_string() call! This code does not work.", E_USER_ERROR)) ? "" : "")); 
        $pass_new = md5( $pass_new ); 

        // Update database 
        $insert = "UPDATE `users` SET password = '$pass_new' WHERE user = '" . dvwaCurrentUser() . "';"; 
        $result = mysqli_query($GLOBALS["___mysqli_ston"],  $insert ) or die( '<pre>' . ((is_object($GLOBALS["___mysqli_ston"])) ? mysqli_error($GLOBALS["___mysqli_ston"]) : (($___mysqli_res = mysqli_connect_error()) ? $___mysqli_res : false)) . '</pre>' );

        // Feedback for the end user 
        echo "<pre>Password Changed.</pre>"; 
    } 
    else { 
        // Issue with the passwords matching 
        echo "<pre>Passwords did not match.</pre>"; 
        $hide_form = false; 
    } 

    ((is_null($___mysqli_res = mysqli_close($GLOBALS["___mysqli_ston"]))) ? false : $___mysqli_res); 
} 

?> 

```

### High
```
攻擊測試步驟::
使用burpsuite攔截封包並修改封包
將step=1修改為step=2,再增加&passed_captcha=true,
再修改程式碼檢查參數
recaptcha_response_field=hidd3n_valu3
User-Agent:reCAPTCHA
即可略過CAPTCHA驗證
```

關鍵程式碼分析
```
<?php 

if( isset( $_POST[ 'Change' ] ) ) { 
    // Hide the CAPTCHA form 
    $hide_form = true; 

    // Get input 
    $pass_new  = $_POST[ 'password_new' ]; 
    $pass_conf = $_POST[ 'password_conf' ]; 

    // Check CAPTCHA from 3rd party 
    $resp = recaptcha_check_answer( 
        $_DVWA[ 'recaptcha_private_key' ], 
        $_POST['g-recaptcha-response'] 
    ); 

    if ( 
        $resp ||  
        ( 
            $_POST[ 'g-recaptcha-response' ] == 'hidd3n_valu3' 
            && $_SERVER[ 'HTTP_USER_AGENT' ] == 'reCAPTCHA' 
        ) 
    ){ 
        // CAPTCHA was correct. Do both new passwords match? 
        if ($pass_new == $pass_conf) { 
            $pass_new = ((isset($GLOBALS["___mysqli_ston"]) && is_object($GLOBALS["___mysqli_ston"])) ? mysqli_real_escape_string($GLOBALS["___mysqli_ston"],  $pass_new ) : ((trigger_error("[MySQLConverterToo] Fix the mysql_escape_string() call! This code does not work.", E_USER_ERROR)) ? "" : "")); 
            $pass_new = md5( $pass_new ); 

            // Update database 
            $insert = "UPDATE `users` SET password = '$pass_new' WHERE user = '" . dvwaCurrentUser() . "' LIMIT 1;"; 
            $result = mysqli_query($GLOBALS["___mysqli_ston"],  $insert ) or die( '<pre>' . ((is_object($GLOBALS["___mysqli_ston"])) ? mysqli_error($GLOBALS["___mysqli_ston"]) : (($___mysqli_res = mysqli_connect_error()) ? $___mysqli_res : false)) . '</pre>' );

            // Feedback for user 
            echo "<pre>Password Changed.</pre>"; 

        } else { 
            // Ops. Password mismatch 
            $html     .= "<pre>Both passwords must match.</pre>"; 
            $hide_form = false; 
        } 

    } else { 
        // What happens when the CAPTCHA was entered incorrectly 
        $html     .= "<pre><br />The CAPTCHA was incorrect. Please try again.</pre>"; 
        $hide_form = false; 
        return; 
    } 

    ((is_null($___mysqli_res = mysqli_close($GLOBALS["___mysqli_ston"]))) ? false : $___mysqli_res); 
} 

// Generate Anti-CSRF token 
generateSessionToken(); 

?> 
```
### Impossible

關鍵程式碼分析
```
<?php 

if( isset( $_POST[ 'Change' ] ) ) { 
    // Check Anti-CSRF token 
    checkToken( $_REQUEST[ 'user_token' ], $_SESSION[ 'session_token' ], 'index.php' ); 

    // Hide the CAPTCHA form 
    $hide_form = true; 

    // Get input 
    $pass_new  = $_POST[ 'password_new' ]; 
    $pass_new  = stripslashes( $pass_new ); 
    $pass_new  = ((isset($GLOBALS["___mysqli_ston"]) && is_object($GLOBALS["___mysqli_ston"])) ? mysqli_real_escape_string($GLOBALS["___mysqli_ston"],  $pass_new ) : ((trigger_error("[MySQLConverterToo] Fix the mysql_escape_string() call! This code does not work.", E_USER_ERROR)) ? "" : "")); 
    $pass_new  = md5( $pass_new ); 

    $pass_conf = $_POST[ 'password_conf' ]; 
    $pass_conf = stripslashes( $pass_conf ); 
    $pass_conf = ((isset($GLOBALS["___mysqli_ston"]) && is_object($GLOBALS["___mysqli_ston"])) ? mysqli_real_escape_string($GLOBALS["___mysqli_ston"],  $pass_conf ) : ((trigger_error("[MySQLConverterToo] Fix the mysql_escape_string() call! This code does not work.", E_USER_ERROR)) ? "" : "")); 
    $pass_conf = md5( $pass_conf ); 

    $pass_curr = $_POST[ 'password_current' ]; 
    $pass_curr = stripslashes( $pass_curr ); 
    $pass_curr = ((isset($GLOBALS["___mysqli_ston"]) && is_object($GLOBALS["___mysqli_ston"])) ? mysqli_real_escape_string($GLOBALS["___mysqli_ston"],  $pass_curr ) : ((trigger_error("[MySQLConverterToo] Fix the mysql_escape_string() call! This code does not work.", E_USER_ERROR)) ? "" : "")); 
    $pass_curr = md5( $pass_curr ); 

    // Check CAPTCHA from 3rd party 
    $resp = recaptcha_check_answer( 
        $_DVWA[ 'recaptcha_private_key' ], 
        $_POST['g-recaptcha-response'] 
    ); 

    // Did the CAPTCHA fail? 
    if( !$resp ) { 
        // What happens when the CAPTCHA was entered incorrectly 
        echo "<pre><br />The CAPTCHA was incorrect. Please try again.</pre>"; 
        $hide_form = false; 
        return; 
    } 
    else { 
        // Check that the current password is correct 
        $data = $db->prepare( 'SELECT password FROM users WHERE user = (:user) AND password = (:password) LIMIT 1;' ); 
        $data->bindParam( ':user', dvwaCurrentUser(), PDO::PARAM_STR ); 
        $data->bindParam( ':password', $pass_curr, PDO::PARAM_STR ); 
        $data->execute(); 

        // Do both new password match and was the current password correct? 
        if( ( $pass_new == $pass_conf) && ( $data->rowCount() == 1 ) ) { 
            // Update the database 
            $data = $db->prepare( 'UPDATE users SET password = (:password) WHERE user = (:user);' ); 
            $data->bindParam( ':password', $pass_new, PDO::PARAM_STR ); 
            $data->bindParam( ':user', dvwaCurrentUser(), PDO::PARAM_STR ); 
            $data->execute(); 

            // Feedback for the end user - success! 
            echo "<pre>Password Changed.</pre>"; 
        } 
        else { 
            // Feedback for the end user - failed! 
            echo "<pre>Either your current password is incorrect or the new passwords did not match.<br />Please try again.</pre>"; 
            $hide_form = false; 
        } 
    } 
} 

// Generate Anti-CSRF token 
generateSessionToken(); 

?> 

```
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
