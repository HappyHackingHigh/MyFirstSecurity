
# 主題一:classical ciphers古典密碼及其破密分析

# 主題二:現代密碼  快速入門篇

>* 本課程模組將分享現代密碼加解密的基本觀念與實測
>* 本課程將以簡單觀念介紹為主,相關演算法細節則請上大學修密碼學課程
>* 本課程將主要以openssl來示範操作現代密碼的加解密

## openssl

```
OpenSSLhttps://zh.wikipedia.org/wiki/OpenSSL
https://www.openssl.org/
https://github.com/openssl/openssl

```

```
OpenSSL is a robust, commercial-grade, and full-featured toolkit for the Transport Layer Security (TLS) 
and Secure Sockets Layer (SSL) protocols. 

It is also a general-purpose cryptography library.
```



## 對稱式密碼 symmetric key algorithms  Private-key cryptography

### DES
```
https://zh.wikipedia.org/wiki/資料加密標準
```
```
DES是一種對稱密鑰加密塊密碼(Block cipher)演算法
1976年被美國聯邦政府國家標準局(NIST)確定為聯邦資料處理標準（FIPS），隨後在國際上廣泛流傳。
```

## 非對稱式密碼 asymmetric key algorithms Public-key cryptography

```
https://en.wikipedia.org/wiki/Public-key_cryptography

RSA
ElGamal
elliptic curve techniques 
```
## RSA
```
维基百科  https://zh.wikipedia.org/wiki/RSA加密演算法
https://www.slideshare.net/shafaan/public-key-cryptography-and-rsa
```
```
RSA加密演算法- 维基百科
RSA加密演算法是一種非對稱加密演算法。在公開金鑰加密和電子商業中RSA被廣泛使用。
RSA是1977年由羅納德·李維斯特（Ron Rivest）、阿迪·薩莫爾（Adi Shamir）和倫納德·阿德曼（Leonard Adleman）一起提出的。
當時他們三人都在麻省理工學院工作。RSA就是他們三人姓氏開頭字母拼在一起組成的。
```

### 簡單範例:請使用python完成底下的實測

步驟一:Key generation(產生key pair)
```
(1)Select primes p=17, q=11
(2)Compute n=pq=187
(3)Compute φ(n)=(p-1)(q-1)=160
(4)Select e=7  ==> GCD(7,160)=1
(5)Compute d: d=23 ==>7*23 mod 160=1 (use the extended Euclid’s algorithm)

公鑰pub={e,n}={7,187}
私鑰pri={d,n}={23,187}
```
步驟二:加密
```
明文M=88
加密(Encrypt): 88^7mod 187
88^7mod 187 =  11(密文C)
```
步驟三:解密
```
解密Decrypt   C=11: 11^23mod 187
M=11^23 mod 187=88
```
### 在google colab的實測
```
https://colab.research.google.com/drive/15rQcJzej3VOr3KlisBcyPoCY6XovqObb#scrollTo=4kP9L_iR4Oge
```
### RSA的安全基礎==>要花很多時間才可完成的大質因數分解

```
好用的線上網站(WebSite)==>factordb.com (質因數分解:分解 N=p*q)

好用的工具(Tools)
Sage(好用的數學計算工具)
Yafu(用來進行大質因數分解)
```

# 主題三:現代密碼之破密分析[請參加HackingWeekend]

### 基礎RSA破密分析[選擇性]

>* Twin Prime的RSA破密分析
>* common factor attack
>* 加密指數攻擊:Hastad’s Broadcast Attack
>* 模數攻擊:common modulus attack
