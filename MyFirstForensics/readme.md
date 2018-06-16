# Forensics

# Forensics領域
>* 
>* 
>* 
>* 
>* cloud Forensics
>* Android Forensics
>* iOS Forensics

# Forensics Tools

### Forensics Platform

[Running REMnux-Provided Images](https://remnux.org/docs/containers/run-apps/)

# file/media Forensics

>* http://www.sleuthkit.org/
>* http://www.sleuthkit.org/autopsy/
>* https://github.com/sleuthkit/autopsy



>* http://www.megabeets.net/csaw-2016-clams-dont-dance-writeup/


# Network Forensics


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
