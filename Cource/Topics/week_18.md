# 1.滲透測試Penetration Testing(PT)

>* https://en.wikipedia.org/wiki/Penetration_test
>* http://devco.re/services/penetration-test
```
滲透測試是指一個具備資安知識與經驗、技術人員受*僱主*所託，
為僱主的網路設備、主機，模擬駭客的手法對網路或主機進行攻擊測試，
為的是發掘系統漏洞、並提出改善方法
```

### 滲透測試方法論Penetration Testing::Standard|Framework

https://www.owasp.org/index.php/Penetration_testing_methodologies

滲透測試有許多方法論與工具,本體驗營先讓你感受到她的魅力,以後再繼續深造! 

>* [Penetration Testing Execution Standard (PTES)](http://www.pentest-standard.org/index.php/Main_Page)
>* PCI Penetration testing guide
>* PCI DSS Penetration Testing guidance
>* PCI DSS Penetration Testing Requirements
>* Penetration Testing Framework
>* Technical Guide to Information Security Testing and Assessment (NIST800-115)
>* Information Systems Security Assessment Framework (ISSAF)
>* Open Source Security Testing Methodology Manual (OSSTMM)
>* [Offensive（Web）Testing Framework《OWTF》2012](https://github.com/7a/owtf)


### 滲透測試主要步驟[簡化版]

### 滲透測試平台與相關工具Penetration Testing Platform:Kali Linux

>* Kali Linux是植基於Debian的Linux發行版，被設計用於滲透測試的攻擊平台。
>* Kali Linux預設安裝了許多滲透測試軟體[300+]，包括nmap (埠掃描器)、Wireshark (封包分析器)、John the Ripper (密碼破解),以及Aircrack-ng (無線區域網路滲透測試軟體) 。 
>* 使用者可透過硬碟、live CD或live USB執行Kali Linux。
>* Kali Linux既有32位元和64位元的Image。可用於x86 指令集。
>* Kali Linux還有基於ARM架構的image，可用於樹莓派Raspberry Pi 這種超小型的電腦。

>* Kali Linux 2018.2 (2018.4.30)
>* https://www.concise-courses.com/hacking-tools/top-ten/

### 滲透測試平台與相關工具 Namp::Network Mapper

>* https://nmap.org/
>* NMAP是一個用於情資蒐集的網路掃描器。
>* 最初由Gordon Lyon用於目標偵測和服務的一項網路技術 。 
>* 基本原理:Nmap發送特製的封包至目標主機，然後分析其反應。
>* Nmap有許多功能，可用來探測網路，包括目標偵測和服務偵測以及作業系統偵測。
>* NMAP提供更高階的腳本漏洞檢測(NSE, nmap script engineering)

NSE(Nmap Script Engine)
```
–提供執行腳本程式(script)環境
–Nmap NSE的腳本程式(script)是使用LUA程式開發的–支援Nmap 網路發掘功能
–支援Nmap 系統偵測判別功能
–可自行撰寫檢測腳本、使用網路上提供之安全腳本
–不同版本會有新增與刪除狀況
–早期nmap支援的nse是smb-check-vulns.nse可以一次找相關漏洞 ！新版的nmap已經取消這個腳本程式(script)!
–https://nmap.org/nsedoc/categories/exploit.html
```

NSE(Nmap Script Engine)功能:
```
Network discovery
Vulnerability detection
Backdoor detection
Vulnerability exploitation
```
##### 使用NSE(Nmap Script Engine)

```
nmap –script smb-vuln-ms08-067.nse  -p445     <XP IP>
```

>* https://resources.infosecinstitute.com/nmap/
>* https://resources.infosecinstitute.com/nmap-cheat-sheet

### 滲透測試平台與相關工具metasploit framework

>* https://github.com/rapid7/metasploit-framework
>* https://www.metasploit.com/
>* https://zh.wikipedia.org/wiki/Metasploit
>* Metasploit可在Windows 、Linux、MacOS 等作業系統下使用
>* 開放原始碼,定期發佈更新
>* 可將攻擊程式模組化,且模組可自行擴充
>* 開發程式語言是ruby,目前已有3300+種攻擊項目

支援匯入漏洞掃描資料
```
1.Foundstone
2.Microsoft-MBSA 
3.Nessus
4.Qualys 
5.Nmap 
6.Retina
```

預先處理:第一次執行msfconsole時先執行下列步驟
```
啟動postgresql資料庫伺服器
Service postgresql start
msfdb init
```

>* MSFconsole Commands(msfconsole的各種指令)(https://www.offensive-security.com/metasploit-unleashed/msfconsole-commands/)
>* msfconsole的各種指令(https://hk.saowen.com/a/9454bb02e5959d4e1c3a7054b23e9743da6b456a9a4eb2816520b1ec5c1ce706)
>* [ABILITIES INC - METASPLOIT BASICS](https://www.blackhat.com/us-18/training/schedule/index.html#abilities-inc---metasploit-basics-9803)

# 2.系統安全攻防錄與Windows XP滲透測試之旅

### 2.1.Kali Linux攻擊之旅

##### 探勘目標平台==>nmap

確認遠方目標平台的作業系統==> nmap -O IP

確認遠方目標平台開啟的服務==> nmap -p 0-65535 IP

確認遠方目標平台是否存在有漏洞==> 使用NSE(Nmap Script Engine)

>* 單一漏洞 vs 漏洞掃描vuln.scanner
>* Nmap Script預設存於/usr/local/share/namp/scripts

搜尋nmap內的scripts名稱
```
ls /usr/local/share/nmap/scripts/ | grep smb
```

##### Exploitation攻擊目標平台(上課講,不公開)

搜尋ms08_067攻擊模組==>search ms08_067

搜尋ms17_010攻擊模組==>search ms17_010

使用ms08_067_netapi攻擊模組==>  use ........

##### Post_exploitation:控制目標平台:meterpreter(上課講,不公開)

檢查入侵到哪一個目錄夾==>pwd


### 2.2.Windows XP 防禦技術

### Step1:檢查網路連線
```
net view
net session /?
net session /list
net session /delete
```

檢查連線到你主機的外來客==> netstat -ano


### Step2:斷絕不肖客的連線==>使用taskkill斷絕連線

檢查taskkill指令參數==>taskkill /?

檢查連線到你主機的外來客==>netstat -ano

找出PID(process ID)並強力斷絕其連線==>taskkill /F /PID XXX

### Step3:升級到最新版本是最簡易做法










