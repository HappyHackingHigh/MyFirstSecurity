# 資安情境 ==> 你是CSO要如何處理??

[1]你管理的Linux被不肖客當作C&C server
>* [2017-04-25國際刑警組織：東南亞窩藏超過8800台的C&C惡意伺服器](https://www.ithome.com.tw/news/113695)
>* [2017-05-08新殭屍大軍Bondnet控制手法再升級，不只發動DDoS攻擊，還派去採礦大賺數位貨幣](https://www.ithome.com.tw/news/113951)

[2]你是金控業者雇用的網管人員,你要如何報告這些可能面對的事件(特別是資安管理法已經通過三讀2018/6/17)

>* [2016一銀ATM遭駭事件大剖析](https://www.ithome.com.tw/article/107291)
>* [2017【遠銀遭駭追追追】](https://www.ithome.com.tw/article/117399)

[2018.5資安法立院三讀通過](https://www.ithome.com.tw/article/123364)

[2018歐盟最嚴格個資規範GDPR正式上路](https://www.ithome.com.tw/article/123464)

[3]你被賦予任務要組電腦安全事件回應小組CSIRT(Computer Security Incident Response Team),如何做?

>* [企業資安急先鋒CSIRT](https://www.ithome.com.tw/article/115714)
>* [NIST 800-61:Computer Security Incident Handling Guide](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-61r2.pdf)
>* [CMU::Computer	Security	Incident	Response	Plan](https://www.cmu.edu/iso/governance/procedures/docs/incidentresponseplan1.0.pdf)

IRM (Incident Response Methodologies)

>* https://github.com/certsocietegenerale/IRM#irm-incident-response-methodologies



# Forensics



# Forensics領域
>* 
>* 
>* 
>* 
>* cloud Forensics
>* Android Forensics
>* iOS Forensics

# Forensics Tools and Platform

### Forensics Platform

>* [Linux Live CD for Forensics](https://techtalk.gfi.com/top-20-free-digital-forensic-investigation-tools-for-sysadmins/)
>* [SANS Investigative Forensic Toolkit] (http://digital-forensics.sans.org/community/downloads
>* [Running REMnux-Provided Images](https://remnux.org/docs/containers/run-apps/)

### Forensics Tools
>* [digital forensics tools](https://forensiccontrol.com/resources/free-software/)

### Learning materials:
>* [歐盟enisa技術培訓內容](https://www.enisa.europa.eu/topics/trainings-for-cybersecurity-specialists/online-training-material/technical-operational)


# File/media Forensics

Autospy and 
>* http://www.sleuthkit.org/
>* http://www.sleuthkit.org/autopsy/
>* https://github.com/sleuthkit/autopsy

Foremost, scalpel 

####  learning Autospy From CTF:csaw-2016-clams-dont-dance

https://github.com/Alpackers/CTF-Writeups/blob/master/2015/CSAW-CTF/Forensics/Flash/Flash%20option%202.md

>* http://www.megabeets.net/csaw-2016-clams-dont-dance-writeup/

http://s0ngsari.tistory.com/entry/CSAW-2016-Clams-Dont-Dance

http://blog.indonesiancoder.com/write-up-csaw-ctf-qualification-round-2016

https://github.com/ctfs/write-ups-2016/tree/master/csaw-ctf-2016-quals/forensics/clams-dont-dance-100

https://github.com/krx/CTF-Writeups/tree/master/CSAW%2016%20Quals/for100%20-%20Clams%20Dont%20Dance

https://github.com/73696e65/ctf-notes/blob/master/2016-ctf.csaw.io/forensics-100-clams_dont_dance.md


### file/media Forensics:Autospy

[Forensics with Autopsy](https://www.youtube.com/watch?v=Z8p3IMxLMTI)

# Network Forensics

#### Network Forensics Tools:

Xplico is an open source Network Forensic Analysis Tool (NFAT) that aims to extract applications data from internet traffic (e.g. Xplico can extract an e-mail message from POP, IMAP or SMTP traffic). Features include support for a multitude of protocols (e.g. HTTP, SIP, IMAP, TCP, UDP), TCP reassembly, and the ability to output data to a MySQL or SQLite database, amongst others.

#### Python Network Forensics

# Memory Forensics

# Memory Forensics:references

[Analyze .NET Framework memory issues](https://msdn.microsoft.com/en-us/library/dn342825.aspx)

## Memory Forensics:　Tools

>* http://www.forensicswiki.org/wiki/Tools:Memory_Analysis

#### DumpIt 

DumpIt provides a convenient way of obtaining a memory image of a Windows system even if the investigator is not physically sitting in front of the target computer. It’s so easy to use, even a naive user can do it. It’s not appropriate for all scenarios, but it will definitely make memory acquisition easier in many situations.

#### Volatility

>* https://github.com/volatilityfoundation/volatility
>* BOOKS:The Art of Memory Forensics
>* 測試範例:有些已經失效

https://www.memoryanalysis.net/amf

https://github.com/volatilityfoundation/volatility/wiki/Memory-Samples


####  [Rekall Framework](http://www.rekall-forensic.com/docs/Manual/overview.html)

>* https://github.com/google/rekall
>* www.rekall-forensic.com
>* http://www.rekall-forensic.com/docs/Manual/tutorial.html

>* The Rekall Framework is a completely open collection of tools, implemented in Python under the GNU General Public License, for the extraction of digital artifacts from volatile memory (RAM) samples. 
>* The extraction techniques are performed completely independent of the system being investigated but offer visibilty into the runtime state of the system. 
>* The framework is intended to introduce people to the techniques and complexities associated with extracting digital artifacts from volatile memory samples and provide a platform for further work into this exciting area of research.

#### Redline

>* https://www.fireeye.com/services/freeware/redline-download-confirmation.html
>* [Memory Analysis Using Redline](http://resources.infosecinstitute.com/memory-analysis-using-redline/#gref)

https://www.fireeye.com/services/freeware/redline-download-confirmation.html

[Top 20 Free Digital Forensic Investigation Tools for SysAdmins](https://techtalk.gfi.com/top-20-free-digital-forensic-investigation-tools-for-sysadmins/)



## 實務演練(1): Volatility memory forensics

#### 測試案例分析:

The Art of Memory Forensics 網站提供的案例https://www.memoryanalysis.net/amf

## 實務演練(2):rekall memory forensics

#### 測試環境1:使用Docker rekall image

```
1.下載:: docker pull remnux/recall

2. run "rekall" in the container with the desired parameters.
sudo docker run --rm -it -v ~/files:/home/nonroot/files remnux/rekall bash

Before running the command above, create the "files" directory on your host and make it world-accessible (e.g., "chmod a+xwr ~/files").

3. To use Rekall's web console, invoke the container with the -p parameter to give your host access to the container's TCP port 8000 like this:

sudo docker run --rm -it -p 8000:8000 -v ~/files:/home/nonroot/files remnux/recall

Then connect to http://localhost:8000 using a web browser from your host.

```

#### 測試環境2

```
$ virtualenv  /tmp/MyEnv
New python executable in /tmp/MyEnv/bin/python
Installing setuptools, pip...done.

$ source /tmp/MyEnv/bin/activate
$ pip install --upgrade setuptools pip wheel
$ pip install rekall


To be able to run the ipython notebook, you will need to install the rekall-gui package:

$ pip install rekall-gui

```
#### 測試案例分析:

>* http://memory-analysis.rekall-forensic.com/www/TOC/
>* https://github.com/scudette/memory-analysis
```
$ git clone https://github.com/scudette/memory-analysis.git
$ cd source
$ python ./runme.py
```




## Learning Memory Forensics from CTF

#### SECCON CTF Quals 2016 : memory-analysis-100

https://github.com/ctfs/write-ups-2016/tree/master/seccon-ctf-quals-2016/forensic/memory-analysis-100



####  CAMP CTF 2015: APT-incident-response-400

https://github.com/ctfs/write-ups-2015/tree/master/camp-ctf-2015/forensics/APT-incident-response-400

#### Nuit du Hack Quals CTF 2015: Bpythonastic

https://github.com/ctfs/write-ups-2015/tree/master/nuit-du-hack-ctf-quals-2015/forensic/bpythonastic

http://ipushino.blogspot.tw/2015/04/ndh-ctf-2015-bpythonastic.html

### Android Forensics
[Live Memory Forensics on Android devices](https://www.slideshare.net/nikoskapios/live-memory-forensics-on-android-devices)

```
```
PDF

CSAW CTF 2014: Obscurity
