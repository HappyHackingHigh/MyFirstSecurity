## 第八週	編碼與解碼

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



# 編碼與解碼:

編碼與解碼是資訊領域常使用的技術

Ascii、Base64、Base32各有其適用處

# encode_and_decode_1:
>*  Ascii 20
>*  ASCII(American Standard Code for Information Interchange)美國資訊交換標準代碼是基於拉丁字母的一套電腦編碼系統
>*  ASCII是現今最通用的單字元編碼系統。
>*  https://en.wikipedia.org/wiki/ASCII
>*  https://www.asciitable.com/
>*  https://www.w3schools.com/charsets/ref_html_ascii.asp

https://www.dcode.fr/ascii-code

# encode_and_decode_2:
>* Base64 20
>* https://en.wikipedia.org/wiki/Base64
>* 使用線上工具解題
>* 使用python程式解題


# encode_and_decode_3:

>* Base32 20
>* https://en.wikipedia.org/wiki/Base32


# encode_and_decode_4:

>* Morse code 20
>* https://en.wikipedia.org/wiki/Morse_code
>* 使用線上工具解題
```
https://morsecode.scphillips.com/translator.html
```

# encode_and_decode_5:

>*  angstromCTF 2016 : what-the-hex 20
>* 

### 使用指令解題 
解題步驟1:

```
echo "6236343a20615735305a584a755a58526659323975646d567963326c76626c3930623239736331397962324e72" | xxd -r -p
```

解題步驟2:
```
echo aW50ZXJuZXRfY29udmVyc2lvbl90b29sc19yb2Nr | base64 -d
```
### 使用python解題:使用標準函示庫base64
```
>>>import base64
>>>‘6236343a20615735305a584a755a58526659323975646d567963326c76626c3930623239736331397962324e72’.decode(“hex”)
>>>base64.b64decode('nnnnnnnnnnn')
```

# encode_and_decode_6:

>*  Internetwache CTF 2016: The hidden message 50
>*  https://www.xil.se/post/internetwache-2016-misc-50-arturo182/
>*  8進位==>轉成字串(Octal to string)==>再base64

解題步驟1:
```
0000000 126 062 126 163 142 103 102 153 142 062 065 154 111 121 157 113
0000020 122 155 170 150 132 172 157 147 123 126 144 067 124 152 102 146
0000040 115 107 065 154 130 062 116 150 142 154 071 172 144 104 102 167
0000060 130 063 153 167 144 130 060 113 012
0000071
```
使用線上工具解題 ==> http://www.unit-conversion.info/texttools/octal/

使用python解題
```
import string

res = ''
f = open('README.txt')
for line in f:
    res = res + ''.join([chr(string.atoi(x, base=8)) for x in line.split(' ')[1::]])

print res
```
