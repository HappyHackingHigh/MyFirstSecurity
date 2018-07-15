駭客隱身術(MyFirstSteganography)

https://en.wikipedia.org/wiki/Steganography

https://en.wikipedia.org/wiki/Steganography_tools

# Steg-100_文件隱寫術

# Steg-101
>*  CSAW QUALS 2015: keep-calm-and-ctf(必)50

解題步驟1:查看檔案格式
```
file /root/Desktop/img.jpg
```

解題步驟2:查看檔案內藏的字串
```
strings /root/Desktop/img.jpg
```
解題步驟3:安裝工具並學習使用技術

google搜尋jpg metadata linux
>* http://xahlee.info/img/metadata_in_image_files.html
>* http://libre-software.net/edit-image-metadata-on-linux/

```
sudo apt-get install exiftool
```

解題步驟4:查看檔案並讀出答案


```
exiftool img.jpg
```

# Steg-102
>* ABCTF 2016 : just-open-it(必) 50

解題步驟1:查看檔案格式

解題步驟2:查看檔案內藏的字串
```
strings just_open_it.jpg | grep ABCTF
```

# Steg-103_黑白色塊隱藏的秘密

>* CSAW Quals CTF 2013: Black & White 50

解題步驟1:查看檔案格式

解題步驟2:查看檔案內藏的字串

解題步驟3:打開檔案看看

解題步驟4:使用stegsolve調色階
```
https://aur.archlinux.org/packages/stegsolve/

the flag in the blue, red or green 0 pane
```
```
#!/bin/bash -ex

wget http://www.caesum.com/handbook/Stegsolve.jar -O stegsolve.jar
chmod +x stegsolve.jar
mkdir bin
mv stegsolve.jar bin/
```

# Steg_104_史上最有名的吃香蕉小朋友

>* sCTF 2016 Q1 : banana-boy-20(必) 50
>* https://github.com/ctfs/write-ups-2016/tree/master/sctf-2016-q1/forensic/banana-boy-20
>* http://blog.csdn.net/riba2534/article/details/70544076
>* https://github.com/nbrisset/CTF/tree/master/sctf-2016-q1/challenges/banana-boy-20

解題步驟1:查看檔案格式

解題步驟2:使用hex編輯器分析檔案

解題步驟3:使用binwalk分析檔案

>* https://github.com/devttys0/binwalk
>* http://www.freebuf.com/sectool/15266.html

```
binwalk carter.jpg
```
解題步驟4:使用dd抽出檔案
```
dd if=carter.jpg of=carter-1.jpg skip=140147 bs=1
```

>* if是指定輸入檔
>* of是指定輸出檔
>* skip是指定從輸入檔開頭跳過140147個塊後再開始複製
>* bs設置每次讀寫塊的大小為1位元組 

解題步驟4b:也可以使用foremost抽出檔案

foremost是一個基於檔檔頭和尾部資訊以及檔的內建資料結構恢復檔的命令列工具
```
[1]Linux安裝：apt-get install foremost
[2]查看使用方式:foremost -help
[3]檔案分離:foremost carter.jpg
```
foremost會自動生成output目錄存放分離檔

解題步驟5:從抽離出的檔案中讀出答案


### hex編輯器
```
Windows平台:winhex,UltraEdit
Linux平台:hexedit, hexdump
安裝hexedit==>sudo apt install ncurses-hexedit
```
### binwalk

### dd

>* https://en.wikipedia.org/wiki/Dd_(Unix)
>* http://blog.csdn.net/riba2534/article/details/70544076
>* http://www.cnblogs.com/qq78292959/archive/2012/02/23/2364760.html

```
if=file #輸入檔案名稱，預設為標準輸入。 
of=file #輸出檔案名稱，預設為標準輸出。 
ibs=bytes #一次讀入 bytes 個位元組(即一個塊大小為 bytes 個位元組)。 
obs=bytes #一次寫 bytes 個位元組(即一個塊大小為 bytes 個位元組)。 
bs=bytes #同時設置讀寫塊的大小為 bytes ，可代替 ibs 和 obs 。 
cbs=bytes #一次轉換 bytes 個位元組，即轉換緩衝區大小。 
skip=blocks #從輸入檔開頭跳過 blocks 個塊後再開始複製。 
seek=blocks #從輸出檔開頭跳過 blocks 個塊後再開始複製。(通常只有當輸出檔是磁片或磁帶時才有效)。 
count=blocks #僅拷貝 blocks 個塊，塊大小等於 ibs 指定的位元組數。 
conv=conversion[,conversion...] #用指定的參數轉換檔。
```

# Steg_105_黑洞隱藏術

BITSCTF 2017 : black-hole-10 20

>* https://github.com/ctfs/write-ups-2017/tree/master/bitsctf-2017/forensic/black-hole-10
>* https://github.com/USCGA/writeups/tree/master/online_ctfs/bitsctf_2017/black_hole
>* https://github.com/nbrisset/CTF/tree/master/bitsctf-2017/challenges/black-hole-10_lily_flac


解題步驟1:


解題步驟2:
```
root@kali:~/Desktop# strings black_hole.jpg 
JFIF
$3br
%&'()*456789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
	#3R
&'()*56789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
}#Q-
………………………………………………..
M$Wh
UQklUQ1RGe1M1IDAwMTQrODF9
ZI;Z+
e!K]z
>}v#y=
&XSlP
7*qm
```
解題步驟3:
```
root@kali:~/Desktop# python 
Python 2.7.14 (default, Sep 17 2017, 18:50:44) 
[GCC 7.2.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import base64
>>> base64.b64encode('BITSCTF')
'QklUU0NURg=='
```
解題步驟4:
```
root@kali:~/Desktop# strings black_hole.jpg 
JFIF
$3br
%&'()*456789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
	#3R
&'()*56789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
}#Q-
………………………………………………..
M$Wh
UQklUQ1RGe1M1IDAwMTQrODF9
ZI;Z+
e!K]z
>}v#y=
&XSlP
7*qm
```
解題步驟5:
```
root@kali:~/Desktop# python
Python 2.7.14 (default, Sep 17 2017, 18:50:44) 
[GCC 7.2.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import base64
>>> base64.b64decode('QklUQ1RGe1M1IDAwMTQrODF9')
```


# Steg_106_錯置的檔案

ABCTF 2016 : gz-30 60

解題步驟1:查看檔案格式
```
root@kali:~/Desktop# file flag
flag: gzip compressed data, was "flag", last modified: Sun Jun 26 17:22:38 2016, from Unix
```
解題步驟2:
```
root@kali:~/Desktop# mv flag flag.gz
```
解題步驟3:
```
root@kali:~/Desktop# gzip -d flag.gz
```
解題步驟4:
```
root@kali:~/Desktop# cat  flag
```

### gzip命令
gzip命令用來壓縮檔案。gzip是個使用廣泛的壓縮程式，檔經它壓縮過後，其名稱後面會多處“.gz”副檔名。

gzip是在Linux系統中經常使用的一個對檔進行壓縮和解壓縮的命令，既方便又好用。gzip不僅可以用來壓縮大的、較少使用的檔以節省磁碟空間，還可以和tar命令一起構成Linux作業系統中比較流行的壓縮檔格式。據統計，gzip命令對文字檔有60%～70%的壓縮率。減少檔大小有兩個明顯的好處，一是可以減少存儲空間，二是通過網路傳輸檔時，可以減少傳輸的時間。

gzip命令的常用選項
```
-c，--stdout將解壓縮的內容輸出到標準輸出，原檔案保持不變
-d，--decompress解壓縮
-f，--force強制覆蓋舊檔案
-l，--list列出壓縮包內儲存的原始檔案的資訊（如，解壓後的名字、壓縮率等）
-n，--no-name壓縮時不儲存原始檔案的檔案名和時間戳，解壓縮時不恢復原始檔案的檔案名和時間戳（此時，解出來的檔案，其檔案名為壓縮包的檔案名）
-N，--name壓縮時儲存原始檔案的檔案名和時間戳，解壓縮時恢復原始檔案的檔案名和時間戳
-q，--quiet抑制所有警告資訊
-r，--recursive遞迴
-t，--test測試壓縮檔案完整性
-v，--verbose冗餘模式（即顯示每一步的執行內容）
-1、-2、...、-9壓縮率依次增大，速度依次減慢，預設為-6

```

# Steg_107_錯誤的檔案

ABCTF 2016 : best-ganondorf-50  60

解題步驟1:查看檔案格式
```
root@kali:~/Desktop# file ezmonay.jpg
ezmonay.jpg: PDP-11 UNIX/RT ldp
```

解題步驟2:上網看看檔案特徵

List of file signatures檔案格式特徵

https://en.wikipedia.org/wiki/List_of_file_signatures

找出jpg的檔案特徵

解題步驟3:使用xxd查看題目的檔案格式
```
root@kali:~/Desktop# xxd ezmonay.jpg | head 
```


解題步驟4:修改成正確的檔案格式
```
root@kali:~/Desktop# printf '\xff\xd8\xff' | dd of=ezmonay.jpg bs=1 seek=0 conv=notrunc
```
解題步驟5:確認是否已經修改正確
```
root@kali:~/Desktop# file ezmonay.jpg
ezmonay.jpg: JPEG image data
```

```
root@kali:~/Desktop# xxd ezmonay.jpg | head 
00000000: ffd8 ff00 4800 4800 00ff db00 4300 0302  ....H.H.....C...
```


解題步驟6:打開修正後的圖片幾可得到解答

### xxd

xxd:將一個檔案以十六進位的形式顯示出來
```
xxd -h

Usage:
       xxd [options] [infile [outfile]]
    or
       xxd -r [-s [-]offset] [-c cols] [-ps] [infile [outfile]]
```
```
Options:
    -a          toggle autoskip: A single '*' replaces nul-lines. Default off.
    -b          binary digit dump (incompatible with -ps,-i,-r). Default hex.
    -c cols     format <cols> octets per line. Default 16 (-i: 12, -ps: 30).
    -E          show characters in EBCDIC. Default ASCII.
    -e          little-endian dump (incompatible with -ps,-i,-r).
    -g          number of octets per group in normal output. Default 2 (-e: 4).
    -h          print this summary.
    -i          output in C include file style.
    -l len      stop after <len> octets.
    -o off      add <off> to the displayed file position.
    -ps         output in postscript plain hexdump style.
    -r          reverse operation: convert (or patch) hexdump into binary.
    -r -s off   revert with <off> added to file positions found in hexdump.
    -s [+][-]seek  start at <seek> bytes abs. (or +: rel.) infile offset.
    -u          use upper case hex letters.
    -v          show version: "xxd V1.10 27oct98 by Juergen Weigert".
```
# Steg_108

BITSCTF 2017 : flagception-30 50(略)

>* https://github.com/USCGA/writeups/tree/master/online_ctfs/bitsctf_2017/flagception

```
#!/usr/bin/env python

print ''.join([chr(int(i,2)) for i in '1000010 1001001 1010100 1010011 1000011 1010100 1000110 1111011 1100110 0110001 1100001 1100111 1100011 0110011 1110000 1110100 0110001 0110000 1101110 1111101'.split(' ')])
```


