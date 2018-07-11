# 特色選修課程教學綱要

課程設計:
>* 本課程規劃為給非資訊類學生及高中職學生的第一門資訊安全認知課程
>* 本課程強調動手做--從實做中學習與體認到到資訊安全的重要性及基本防護技能


## 第一週	從資訊安全到資訊倫理與法律

## 第二週	Linux安全測試基礎

課程目標:上完這課程模組後,學生要會
>* 了解作業系統的基本觀念[資訊科技概論課程內容]
>* 了解Linux作業系統的核心(kernel)與外殼(Shell)
>* 了解Linux作業系統的發行版本(distribution):Ubuntu/Kali linux
>* 了解Linux作業系統的目錄結構
>* 熟悉Linux的目錄存取的指令:pwd/cd/ 
>* 熟悉Linux的目錄內容的指令:ls及其參數
>* 熟悉Linux的指令參數說明:help/man/網路查詢
>* 熟悉Linux的檔案內容:cat
>* 熟悉Linux的檔案查詢指令:find
>* 熟悉Linux的網路指令:wget/ssh/
>* 熟悉Linux的壓縮解縮與打包指令:tar
>* 熟悉Linux的行程管理指令:ps
>* 完成linux-CTF 題目練習

延伸學習:完成[overTheWire/Bandit](http://overthewire.org/wargames/bandit/)練習

## 第三週	隱寫術
課程目標:上完這課程模組後,學生要會
>* 隱寫術的觀念
>* 隱寫術的類型:文件隱寫術|圖片隱寫術|聲音隱寫術|影片隱寫術|...
>* 完成word文件隱寫術的解題
>* 了解檔案特徵結構(file magic)
>* 熟悉binwalk及dd的使用
>* 完成圖片隱寫術的解題
>* 修復圖片技術及完成圖片隱寫術的解題

延伸學習:[選擇性]
>* Audio steganography(聲音隱寫術)
>* Video steganography(影片隱寫術)

延伸學習:鼓勵學生參加HackingWeekend研習營--Advanced Steganography:From audio to Video課程

## 第四週	加密/解密與破密
課程目標:上完這課程模組後,學生要會
>* 熟悉古典密碼學的凱薩加密與解密
>* 使用線上工具完成古典密碼學的暴力破解法
>* 使用線上工具完成古典密碼學的頻率分析法
>* 熟悉古典密碼學的密碼棒之加密與解密
>* 完成crypto-CTF題目解題

延伸學習:鼓勵學生參加Breakall CTF練習

## 第五週	使用Python進行加解密與破密(1)

>* 本課程適合尚未學過python程式設計的同學,會先教導python程式設計
>* 已修過python程式設計的學校可以進階課程擴充教學

課程目標:上完這課程模組後,學生要會
>* 安裝與熟悉python開發環境[課程教導使用Linux/Python開發環境]
>* 安裝與熟悉windows平台的python開發環境[錄影教學]
>* Python資料型態與運算
>* 迴圈與選擇結構
>* 函數開發技術
>* 使用python程式完成凱薩密碼的解密

進階主題: Python物件導向技術

## 第六週	使用Python進行加解密與破密(2)

課程目標:上完這課程模組後,學生要會
>* 使用Python求解affine cipher破密分析題
>* 使用內建函式解決一般問題
>* 使用python程式完成Crypto-CTF題目
>* 使用標準函式庫hashlib進行MD/SHA1/SHA2562雜湊的應用
>* 安裝第三方函式庫
>* 使用第三方函式庫進行質因數分解
>* 使用第三方函式庫完成Crypto-CTF題目

延伸學習:鼓勵學生參加HackingWeekend研習營--Python程式設計與PPC課程

## 第七週	現代密碼加解密與破密(初體驗)[選擇性課程]

課程目標:上完這課程模組後,學生要會
>* 了解對稱式密碼與非對稱式密碼的觀念
>* 熟悉使用openssl進行DES對稱式密碼的加密與解密
>* 熟悉使用openssl進行RSA非對稱式密碼的加密與解密
>* 熟悉使用Python進行RSA非對稱式密碼的破密[選擇性]
>* 熟悉使用openssl進行MD/SHA1/SHA2562雜湊的應用

進階主題: 基礎RSA破密分析[選擇性]
>* Twin Prime的RSA破密分析
>* common factor attack
>* 加密指數攻擊:Hastad’s Broadcast Attack
>* 模數攻擊:common modulus attack

延伸學習:鼓勵學生參加HackingWeekend研習營--破密分析課程

## [第八週	編碼與解碼](https://github.com/HappyHackingHigh/MyFirstSecurity/blob/master/Cource/Topics/week_8.md)

課程目標:上完這課程模組後,學生要會
>* 熟悉ASCII編碼與解碼原理
>* 使用線上工具完成ASCII CTF基礎題目
>* 熟悉base64編碼與解碼原理
>* 使用線上工具完成base64 CTF基礎題目
>* 使用線上工具完成base32 CTF基礎題目
>* 使用線上工具完成Morse code CTF基礎題目

進階目標:
>* 使用python程式求解編碼與解碼問題
>* 完成CTF進階題目

第九週	期中考

## [第十週	網路安全與封包分析(1)](https://github.com/HappyHackingHigh/MyFirstSecurity/blob/master/Cource/Topics/week_10.md)

課程目標:上完這課程模組後,學生要會
>* [案例教學]連線到google的封包分析或
>* 對TCP/IP網路協定的觀念有基本的認識
>* 安裝Windows版的wireshark
>* 使用wireshark進行封包存檔與載入
>* 使用wireshar分析HTTP封包格式
>* 使用wireshar分析TCP封包格式
>* 使用wireshar分析IP封包格式
>* 使用wireshar分析DNS封包格式
>* 使用wireshar分析UDP封包格式

延伸學習:
>* 使用ping scan完成ICMP封包格式分析
>* 完成TCP協定的三次交握分析
>* 使用FTP到FTP遠端伺服器的封包分析

## 第十一週	網路安全與封包分析(2)

課程目標:上完這課程模組後,學生要會
>* 熟悉wireshark的網路封包分析技術(跟踪TCP stream)
>* 熟悉wireshark的設定技術
>* 網路鑑識(Network Forensic)的基本觀念
>* 完成CTF網路封包的分析題目
>* 完成CTF網路攻擊封包的分析題目

延伸學習:
>* 完成SSL封包分析題目
>* 完成DDOS網路攻擊封包的分析題目

## 第十二週	網路安全之防火牆實務[選擇性課程]

課程目標:上完這課程模組後,學生要會
>* 了解網路防火牆的原理
>* 熟悉網路防火牆的建置[選擇性|影片教學]
>* 熟悉網路防火牆規則的撰寫
>* 熟悉網路防火牆偵測的載入
>* 網路攻防演練設計[選擇性|影片教學]
>* 完成網路攻防演練案例[阻擋攻擊]

延伸學習:上網收集資料並完成使用UFW/Gufw進行網路攻防設計與實測

## 第十三週	網路安全之入侵偵測系統實務[選擇性課程]

課程目標:上完這課程模組後,學生要
>* 了解入侵偵測系統的原理
>* 了解入侵偵測系統的類型:主機型|網路型
>* 熟悉snort入侵偵測系統的建置[選擇性|影片教學]
>* 熟悉snort入侵偵測規則的撰寫
>* 熟悉snort入侵偵測的載入
>* 網路偵測演練設計[選擇性|影片教學]
>* 完成網路偵測演練案例

延伸學習:上網收集資料並完成使用Suricata IDS進行網路偵測設計與實測

## 第十四週[網站安全初體驗](https://github.com/HappyHackingHigh/MyFirstSecurity/blob/master/Cource/Topics/week_14.md)

課程目標:上完這課程模組後,學生要會
>* HTTP協定的基礎實測與分析
>* 熟悉developer Tools網站安全測試工具的使用:示範演練HITCON 2017題目
>* 熟悉Cur網站安全測試工具的使用:完成CTF new HTTP method題目
>* 熟悉使用Burpsuite進行HTTP封包的修改:完成CTF Burpsuite題目
>* 完成Web101-CTF的題目

延伸學習:熟悉網站安全測試工具的使用:OWASP Mantra或HackingBar

## 第十五週	網站漏洞分析(1)[選擇性課程]

課程目標:上完這課程模組後,學生要會
>* OWASP TOP 10(2017年版本)揭露的漏洞之基本認知
>* File inclusion網站漏洞的分析
>* 黑名單過濾法的實務
>* 繞過黑名單過濾法的攻擊測試
>* 完整的資安防禦技術實測

延伸學習:
>* 網站漏洞掃描實務[錄影教學]
>* 鼓勵學生參加HackingWeekend研習營--PHP Security網站安全課程

## 第十六週	網站漏洞分析(2)[選擇性課程]

課程目標:上完這課程模組後,學生要會
>* File upload網站漏洞的分析
>* command injection網站漏洞的分析
>* SQL injection網站漏洞的分析
>* Xss網站漏洞的分析

延伸學習:鼓勵學生參加HackingWeekend研習營--WebSecurity網站安全課程

## 第十七週	網站安全防護實務:WAF[選擇性課程]

課程目標:上完這課程模組後,學生要會
>* 了解網站應用程式防火牆WAF的原理
>* 熟悉Modsecurity網站應用程式防火牆的建置[選擇性|影片教學]
>* 熟悉Modsecurity規則的撰寫
>* 熟悉Modsecurity規則的載入
>* 網站攻防演練設計[選擇性|影片教學]
>* 完成網站攻防演練案例[阻擋SQli攻擊]

延伸學習:上網收集資料並完成使用Modsecurity進行XSS網站攻防演練

## 第十八週	系統安全初體驗

課程需知:
>* 需熟悉linux基本指令{上過第二週	Linux安全測試基礎即可}
>* Kali Linux{預設帳密: root/toor}

課程目標:上完這課程模組後,學生要會
>* 了解滲透測試的觀念
>* Nmap 服務掃描實測
>* Nmap NSE單一漏洞掃描實測 
>* 使用metasploit進行Windows 滲透測試
>* 使用Metepreter指令操控遠端被入侵的Windows
>* Windows的防護技術

延伸學習:
>* linux伺服器安全:完成metasploitable2的攻擊測試
>* Windows伺服器安全:完成metasploitable3的攻擊測試

## 第十九週	人工智慧與資訊安全

第二十週	期末考
