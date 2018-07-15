# 第七週	現代密碼加密與解密

課程目標:上完這課程模組後,學生要會

>* 了解對稱式密碼與非對稱式密碼的觀念
>* 熟悉使用openssl進行DES對稱式密碼的加密與解密
>* 熟悉使用openssl進行RSA非對稱式密碼的加密與解密
>* 熟悉使用openssl進行MD/SHA1/SHA2562雜湊的應用
>* 熟悉使用Python進行RSA非對稱式密碼的加密與解密[選擇性]

# A.使用openssl進行加密與解密

>* 熟悉使用openssl進行DES對稱式密碼的加密與解密
>* 熟悉使用openssl進行RSA非對稱式密碼的加密與解密
>* 熟悉使用openssl進行MD/SHA1/SHA2562雜湊的應用

## openssl
>* https://zh.wikipedia.org/wiki/OpenSSL
>* OpenSSL是一個開放原始碼的軟體函式庫套件
>* 應用程式可以使用這個套件來進行安全通訊，避免竊聽，同時確認另一端連線者的身分。
>* 這個套件廣泛被應用在網際網路的網頁伺服器上。
>* HTTPS是一種協議，等於HTTP+TLS。openssl是一套開源工具集，實現了ssl2，ssl3，TLSv1，TLSv1.1，TLSv1.2協議。
>* 如果是使用apache或者nginx，那就是使用openssl。
>* windows系列的伺服器包括IIS，windows server等都是使用schannel，沒有使用openssl，不會受openssl heartbleed影響。
>* openssl漏洞:openssl heartbleed[2014-4]+ ssl3.0貴賓犬攻擊[Padding Oracle On Downgraded Legacy Encryption（POODLE，貴賓犬）][2014-10]
>* SSL(Secure Sockets Layer)3.0其實是個已被廢棄且不安全的協定，而且多數已被較新的TLS(Transport Layer Security)1.0、TLS 1.1或TLS所取代，然而，有許多系統在導入TSL時都保留了向下相容的能力，以與仍然採用SSL 3.0的老舊系統互動，目的是為了維持流暢的使用者經驗。
>* http://blog.alantsai.net/posts/2017/09/iis-security-set-correct-schannel-and-cipher-suite-using-iis-crypto
>* IIS Crypto
>* 其主要函式庫是以C語言所寫成，實作了基本的加密功能，實作了SSL與TLS協定。
>* OpenSSL可以運行在OpenVMS、 Microsoft Windows以及絕大多數類Unix作業系統上
>* OpenSSL支援許多不同的加密演算法：
```
加密:AES、Blowfish、Camellia、SEED、CAST-128、DES、IDEA、RC2、RC4、RC5、TDES、GOST 28147-89
密碼雜湊函式:MD5、MD4、MD2、SHA-1、SHA-2、RIPEMD-160、MDC-2、GOST R 34.11-94, BLAKE2、Whirlpool
公開金鑰加密:RSA、DSA、迪菲-赫爾曼密鑰交換、橢圓曲線、GOST R 34.10-2001
```
https://github.com/openssl/openssl

#### [動手作1]列出 OpenSSL 提供的指令
```
openssl -h 
openssl -help
openssl --h 
openssl --help
```
三大類型指令:
>* Standard commands:
>* Message Digest commands (see the `dgst' command for more details)
>* Cipher commands (see the `enc' command for more details)
```
Standard commands
asn1parse         ca                ciphers           cms               
crl               crl2pkcs7         dgst              dh                
dhparam           dsa               dsaparam          ec                
ecparam           enc               engine            errstr            
gendh             gendsa            genpkey           genrsa            
nseq              ocsp              passwd            pkcs12            
pkcs7             pkcs8             pkey              pkeyparam         
pkeyutl           prime             rand              req               
rsa               rsautl            s_client          s_server          
s_time            sess_id           smime             speed             
spkac             srp               ts                verify            
version           x509              

Message Digest commands (see the `dgst' command for more details)
md4               md5               rmd160            sha               
sha1              

Cipher commands (see the `enc' command for more details)
aes-128-cbc       aes-128-ecb       aes-192-cbc       aes-192-ecb       
aes-256-cbc       aes-256-ecb       base64            bf                
bf-cbc            bf-cfb            bf-ecb            bf-ofb            
camellia-128-cbc  camellia-128-ecb  camellia-192-cbc  camellia-192-ecb  
camellia-256-cbc  camellia-256-ecb  cast              cast-cbc          
cast5-cbc         cast5-cfb         cast5-ecb         cast5-ofb         
des               des-cbc           des-cfb           des-ecb           
des-ede           des-ede-cbc       des-ede-cfb       des-ede-ofb       
des-ede3          des-ede3-cbc      des-ede3-cfb      des-ede3-ofb      
des-ofb           des3              desx              rc2               
rc2-40-cbc        rc2-64-cbc        rc2-cbc           rc2-cfb           
rc2-ecb           rc2-ofb           rc4               rc4-40            
seed              seed-cbc          seed-cfb          seed-ecb          
seed-ofb          
``` 
#### [動手作2]列出 OpenSSL 提供的資訊摘要(Message Digest)和數位簽章(Digital Signature)

openssl dgst --help
```
unknown option '--help'
options are
-c              to output the digest with separating colons        //輸出的摘要資訊以分號隔離，和-hex同時使用
-r              to output the digest in coreutils format           //指定輸出的格式
-d              to output debug info                               //輸出BIO調試資訊
-hex            output as hex dump                                 //以16進制列印輸出結果
-binary         output in binary form                              //輸出二進位結果
-hmac arg       set the HMAC key to arg                            //指定hmac的key
-non-fips-allow allow use of non FIPS digest                       //允許使用不符合fips標準的摘要演算法
-sign   file    sign digest using private key in file              //執行簽名操作，後面指定私密金鑰檔
-verify file    verify a signature using public key in file        //執行驗證操作，後面指定公開金鑰檔，與prverfify不能同時使用
-prverify file  verify a signature using private key in file       //執行驗證操作，後面指定金鑰檔，與verfify不能同時使用
-keyform arg    key file format (PEM or ENGINE)                    //指定金鑰檔案格式，pem或者engine
-out filename   output to filename rather than stdout              //指定輸出檔，默認標準輸出
-signature file signature to verify                                //指定簽名檔，在驗證簽名時使用
-sigopt nm:v    signature parameter                                //簽名參數
-hmac key       create hashed MAC with key                         //製作一個hmac 使用key
-mac algorithm  create MAC (not neccessarily HMAC)                 //製作一個mac
-macopt nm:v    MAC algorithm parameters or key                    //mac演算法參數或者key
-engine e       use engine e, possibly a hardware device.          //使用硬體或者三方加密庫
-md4            to use the md4 message digest algorithm            //摘要演算法使用md4
-md5            to use the md5 message digest algorithm            //摘要演算法使用md5
-ripemd160      to use the ripemd160 message digest algorithm      //摘要演算法使用ripemd160
-sha            to use the sha message digest algorithm            //摘要演算法使用sha
-sha1           to use the sha1 message digest algorithm           //摘要演算法使用sha1
-sha224         to use the sha224 message digest algorithm         //摘要演算法使用sha223
-sha256         to use the sha256 message digest algorithm         //摘要演算法使用sha256
-sha384         to use the sha384 message digest algorithm         //摘要演算法使用sha384
-sha512         to use the sha512 message digest algorithm         //摘要演算法使用sha512
-whirlpool      to use the whirlpool message digest algorithm      //摘要演算法使用whirlpool
```
#### [動手作]列出 OpenSSL 提供的對稱式加解密演算法

openssl enc –h

注意輸出顯示中的Cipher Types
```
options are
-in <file>     input file
-out <file>    output file
-pass <arg>    pass phrase source
-e             encrypt
-d             decrypt
-a/-base64     base64 encode/decode, depending on encryption flag
-k             passphrase is the next argument
-kfile         passphrase is the first line of the file argument
-md            the next argument is the md to use to create a key
                 from a passphrase.  One of md2, md5, sha or sha1
-S             salt in hex is the next argument
-K/-iv         key/iv in hex is the next argument
-[pP]          print the iv/key (then exit if -P)
-bufsize <n>   buffer size
-nopad         disable standard block padding
-engine e      use engine e, possibly a hardware device.
Cipher Types
-aes-128-cbc               -aes-128-cbc-hmac-sha1     -aes-128-cbc-hmac-sha256  
-aes-128-ccm               -aes-128-cfb               -aes-128-cfb1             
-aes-128-cfb8              -aes-128-ctr               -aes-128-ecb              
-aes-128-gcm               -aes-128-ofb               -aes-128-xts              
-aes-192-cbc               -aes-192-ccm               -aes-192-cfb              
-aes-192-cfb1              -aes-192-cfb8              -aes-192-ctr              
-aes-192-ecb               -aes-192-gcm               -aes-192-ofb              
-aes-256-cbc               -aes-256-cbc-hmac-sha1     -aes-256-cbc-hmac-sha256  
-aes-256-ccm               -aes-256-cfb               -aes-256-cfb1             
-aes-256-cfb8              -aes-256-ctr               -aes-256-ecb              
-aes-256-gcm               -aes-256-ofb               -aes-256-xts              
-aes128                    -aes192                    -aes256                   
-bf                        -bf-cbc                    -bf-cfb                   
-bf-ecb                    -bf-ofb                    -blowfish                 
-camellia-128-cbc          -camellia-128-cfb          -camellia-128-cfb1        
-camellia-128-cfb8         -camellia-128-ecb          -camellia-128-ofb         
-camellia-192-cbc          -camellia-192-cfb          -camellia-192-cfb1        
-camellia-192-cfb8         -camellia-192-ecb          -camellia-192-ofb         
-camellia-256-cbc          -camellia-256-cfb          -camellia-256-cfb1        
-camellia-256-cfb8         -camellia-256-ecb          -camellia-256-ofb         
-camellia128               -camellia192               -camellia256              
-cast                      -cast-cbc                  -cast5-cbc                
-cast5-cfb                 -cast5-ecb                 -cast5-ofb                
-des                       -des-cbc                   -des-cfb                  
-des-cfb1                  -des-cfb8                  -des-ecb                  
-des-ede                   -des-ede-cbc               -des-ede-cfb              
-des-ede-ofb               -des-ede3                  -des-ede3-cbc             
-des-ede3-cfb              -des-ede3-cfb1             -des-ede3-cfb8            
-des-ede3-ofb              -des-ofb                   -des3                     
-desx                      -desx-cbc                  -id-aes128-CCM            
-id-aes128-GCM             -id-aes128-wrap            -id-aes192-CCM            
-id-aes192-GCM             -id-aes192-wrap            -id-aes256-CCM            
-id-aes256-GCM             -id-aes256-wrap            -id-smime-alg-CMS3DESwrap 
-rc2                       -rc2-40-cbc                -rc2-64-cbc               
-rc2-cbc                   -rc2-cfb                   -rc2-ecb                  
-rc2-ofb                   -rc4                       -rc4-40                   
-rc4-hmac-md5              -seed                      -seed-cbc                 
-seed-cfb                  -seed-ecb                  -seed-ofb                 
```
### [實作2] 使用openssl進行 DES 加密與解密

##### 使用 DES 加密

ksu@ksu-VirtualBox:~$ echo test > infile

ksu@ksu-VirtualBox:~$ cat infile

openssl des -in infile -out infile.des
```
執行後，OpenSSL 會提示使用者由鍵盤上輸入加密之密碼，如下:
    enter des-cbc encryption password:
不管鍵盤輸入什麼，畫面上都不會出現任何字元。輸入完成後，按下鍵盤上的 "Enter" 鍵即可。

OpenSSL 會再一次要求使用者輸入一次相同的密碼
加密的檔案將以 infile.des 的名稱存在於磁碟中。
```
ksu@ksu-VirtualBox:~$ cat infile

test

ksu@ksu-VirtualBox:~$ cat infile.des

##### 使用 DES 解密

openssl des -d -in infile.des -out okfile

```
執行後，OpenSSL 會提示使用者由鍵盤上輸入加密之密碼，如下:
    enter des-cbc encryption password:
不管鍵盤輸入什麼，畫面上都不會出現任何字元。輸入完成後，按下鍵盤上的 "Enter" 鍵即可。

OpenSSL 會再一次要求使用者輸入一次相同的密碼
加密的檔案將以 okfile.des 的名稱存在於磁碟中。
```
cat okfile

>* 加密用的密碼和解密的密碼用的都是同一個<====>對稱式密碼

#### [練習] 使用 3DES 加密與解密

>* 只要把上述的des改成des3
```
使用 Triple DES加密 ==> openssl des3 -in myfile -out file.des3
使用 Triple DES解密 ==> openssl des3 -d -in file.des3 -out HIfile
```
##### 參考資料

>* 資料加密標準DES::Data Encryption Standard
>* https://zh.wikipedia.org/wiki/資料加密標準
>* 三重DES(Triple-DES)
>* https://zh.wikipedia.org/wiki/三重資料加密演算法



### [實作3] 使用openssl進行 RSA 加密與解密

```
Step1:生成一個私鑰： openssl genrsa -out test.key 1024
這裡-out指定生成檔的。需要注意的是這個檔包含了公開金鑰和金鑰兩部分，也就是說這個檔即可用來加密也可以用來解密。1024是生成金鑰的長度。

Step2:openssl將檔案中的公開金鑰提取出來： openssl rsa -in test.key -pubout -out test_pub.key
-in指定輸入檔，-out指定提取生成公開金鑰的檔案名。


Step3:在目錄中創建一個hello的文字檔: echo happyhacking > hello

Step4:利用生成的公開金鑰加密檔案：openssl rsautl -encrypt -in hello -inkey test_pub.key -pubin -out hello.en 
-in指定要加密的檔，-inkey指定金鑰，-pubin表明是用純公開金鑰檔加密，-out為加密後的檔。

Step5:解密文件：openssl rsautl -decrypt -in hello.en -inkey test.key -out hello.de
-in指定被加密的檔，-inkey指定私密金鑰檔，-out為解密後的檔。
```
##### 看看rsa有什麼參數可用?

openssl rsa -h
```
unknown option -h
rsa [options] <infile >outfile
where options are
 -inform arg     input format - one of DER NET PEM
 -outform arg    output format - one of DER NET PEM
 -in arg         input file
 -sgckey         Use IIS SGC key format
 -passin arg     input file pass phrase source
 -out arg        output file
 -passout arg    output file pass phrase source
 -des            encrypt PEM output with cbc des
 -des3           encrypt PEM output with ede cbc des using 168 bit key
 -seed           encrypt PEM output with cbc seed
 -aes128, -aes192, -aes256
                 encrypt PEM output with cbc aes
 -camellia128, -camellia192, -camellia256
                 encrypt PEM output with cbc camellia
 -text           print the key in text
 -noout          don't print key out
 -modulus        print the RSA key modulus
 -check          verify key consistency
 -pubin          expect a public key in input file
 -pubout         output a public key
 -engine e       use engine e, possibly a hardware device.
```
##### 產生私鑰genrsa

openssl genrsa -out private.pem
```
Generating RSA private key, 2048 bit long modulus
...................+++
...........................+++
e is 65537 (0x10001)
```
##### 看看私鑰長甚麼樣子?

cat private.pem 
```
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEA1R9rH4C1RngrV1kEu/xSc/rdYTeokT90TZEX+0PHrOCETMjd
xoWoLAFUJ+oyTPpQY8v64r+o5AIh6jKVr3rIno+nI1aScl51L8ikVgXuWSEsdSO9
3+dVMDG6jpddqc19rK05ghB07c2pIdG0lTxEZ2bxrqZ9CYTiMSyFXOPgazWtom8G
TyrHZV1ISQLROeVnlO09T/AMvbKG3/AygBnmIRJ9ERcoEuMCvP2jEczQFY/YUw0F
qTRZET7/DfklE03MSQzykr2IyMXKeUsDjOD5f7YX71H6r8npGAxlOG0NW6s1DEcJ
rs9MnR2wqZlEzIUNp/E6UlM6Kg/oeEyISczHFQIDAQABAoIBAEmK8PVK/cLWfuZC
Yp7YAD/jZndAtJuCkQifM+5RwlqGk0DH47e4sYKV5strRnZHvmvhnK6YQpiDn95o
HD0UmpwUqDFKk3iB3eBiVUsV+tyo1OWLMt9LvZrG3kCMPRb2QRLQJ9MZCLBy0pVH
/w+sX1JrNKT28JjTURZ07YRTYkK7/rJcY582ciaB6UPloiWTfEyl7smIJmiBfLvA
BGhJQaE7Nq6H7oGtW8mU4vrDkraqtXPhnRLAkXbzli7uhHRHA5km/XEurHVwoBoY
ZyB8bgRaK7Bev4HuNKw6UmbHgFhhkuV0HWuwF4wYqZYVKDSKg3yi6J1nQFQvruwb
tGlaM+ECgYEA+BCjoPmNMyoziSATghm7ul19JzlT69A02ZPB0G48mGBt7kILcNdg
BQxyzHNHijHNgrAydim5/SUhXZQ/Yumgr/ZFEal9KtOHTj6vS9CjyUHKUnlNMly+
nYGswOXFmAvroU5SbwyecgdeGr+dfEuwPy+Tz9rh4JhSVrczeLu/c7kCgYEA2/Ck
pd+x9kvNewnuQX58CrHnyh11iilc+JKGp29QcIh5ojmvDOrY8v4zX9ITmrIgt/oY
eyP+ksLu7FnUWDXuLc+NuK2d5XHgHcRx+okREatTbWiWm2wB/qnjougfm0HZMOKE
yYuojEtUL4/p8JRFUJ0VDl06M8dImXFgPAqh1D0CgYEA9FYvVdd4JPVkXaSiknsW
VbLQG1p0NsmVxNmtBcgPF2ej4BJdgoAhq9dfG9JQnOYBLsCuc4UWFSoFe08SQDMu
eyNvVL5E83H2zDMiJuMS8KFEz4d7aie/+RRJPJcV0XWsWe3zdD5Rsq9fGamzTUKg
Dxyl0w4dfkOKlq9Mm5cSNMECgYEAiWZmlbGPzdxBPDJSA9xuxYeq1FtfCLcae7ee
I4+o4wR/aFc9AobcjcE8ewoUcToCsqytCpDMAweAl2ru+0SFzVyynsLnt2VSq4YD
5o4mebFcZydFn0b0YBHmQeldhXK3qpB4gCidXTfaGfSAI2mde+UGOHkJWTuQITvw
8NF7k8kCgYA1hs/88q6mc3+OQcc0+0ZOLgel0UOFAdWRk8YlJ/wE0zHnsBr5cA0l
sqizYQWlftkGnqAzszycOK0bjYCZiBAFzCh3ZYXWrSvP1Arv6QUBw7sY8+63zVRS
KIFa++1hskCfFfJ28DLC64sFsKqkdoxoKCQ4ymZWkt5s0DPj6CqNyw==
-----END RSA PRIVATE KEY-----
```

>* 愈長的私鑰被破解的機率愈低
>* 但使用加密與解密的時間也會愈長

##### 產生1024 bits 私鑰genrsa

openssl genrsa 1024 -out private.pem

openssl genrsa 1024 > private.pem
```
Generating RSA private key, 1024 bit long modulus
...............++++++
..........................................................................++++++
e is 65537 (0x10001)
```
cat private.pem
```
-----BEGIN RSA PRIVATE KEY-----
MIICXQIBAAKBgQDHtk3Pnu3Txu/koFAd6+sEGv3gK/nWDES8/aW8A7bFLAzeFA2j
otPk2HTbML3cG/hH0Tkduc2taGHQERX/KYab3OoNwZb3RNGfB2VG3yLijMvK5D3D
tR5daHF7QM9SSmsMuGGWpghN9Fxlkb4aAqH6/tAxVq1Kcd007ADMiHOxCwIDAQAB
AoGAHNx0rD98gTFrs6+TRG+2m/ZGoCHazhshx+okDGLBBAeUqHdfbTl3w8egQ5js
pyWHoOFUjr4uQhQmpooBkslugVBIoVcW/yyi8gNUHbNAvDSAzYiAaTNzPuh/jOLi
4emUQGFaVX+/EM5HjsjHUmCBqlTh1lc58fgfLEn0nG0OXoECQQDzbJGLGfBGiSoI
aIWQ/oACf0MvazY2wWP7R/VXAKtCcnb3BOZpK1qU+56yE+c5ft42tvKCzluP95PP
yTge6AHBAkEA0geeOVgtrtbHYC7r+bdOlfLYDtVfMfb0MIWTlCD2wb4zl+7XzqyN
YSb1TUuQBDJA5+GVuhqHWy0cvc3vyEONywJBAO4Nn6v0GukwHJ4KcYyhhthqUm7e
Hy+fIsLL1V9XNSSPQk5CSX5SOox2IfUux7KPoorJkRJg8mQxjyjmNG7tH0ECQQCT
vTAbfl+EISjWC6uKWNs6tzwsEwOHjgNvLkcFZ7qrxjNcqHG9u7snn9Plr0V67i6h
7hj4dDjKdg1FplsJMBvJAkAYP0xdCYyhvZWP0XftU1n3c0gqjRorm6yoRcsBrE1Q
wdj55ugyKs4eoyCtl64/LbQFWH27CFfme9mdYuyZNQc3
-----END RSA PRIVATE KEY-----
```
執行第二次的genrsa私鑰會不同
```
-----BEGIN RSA PRIVATE KEY-----
MIICXQIBAAKBgQDCCJbI9mMcMd/OW4EiNhd+umd4Z7qKqNlUtZXra7zvM7WExQRk
v2afF2QS85HFYlTg7tANgbRdoKBQWcOPlmvLreqJJBRYLnOWpHP7vTQgdEtCKtfy
C+2a4KY56N033uCwpSHbKWi1PP7ToyZMm9SIJiIvYVGtk4zIxftCIu8aPQIDAQAB
AoGBAKFo77ZhcHUl8B4D9Np20Pi1LBn3gDCU4aYcIIjk6Ri7lUbLdioxJrc1iCRT
xnHCqQUs5Jo3yckRNAtjgNFTunsTWT7uchyYKUy9rEoUY1gOrcwEqxAoZACFVYdd
MsLr54D6NTiv1TlQtifeutVZG95j6DmWVHlJG+zc7ZpOEszpAkEA8M3eB3ypQsOt
TiuOieV9gGk4P0ckk57RlsxRBGIbXMMVCJEyYQeSvt8Xj5xFi8I39bWDljc/ySzQ
UHNYFGDGewJBAM5HJ1x8lZAHFAHIoTAgToO45EvLTp96f7qTbI5yHSTM/1SsS0Ie
2EqkkFYhV2M8as4wCICqsR6QI54xhsXG4KcCQQC6DKUOLc/syJi++8I+YrQroaAW
q9XjxGJ021mBRHeVnRhELUK6WwqTNHTUvU2yZJWt3tdTGU7MFTbB4cxcukS/AkAG
4JZuXfT6lVHUcWT2Xs1fVOW/pSqc5I+nn8ypvyI7nN4Sa6AitzaM3om1ZW0tcNE6
yJ0v9QDsvO+DEbGlnGjXAkAanrxs81VyGrNykrRkdodPjaf+L64NzA8OMCG45IaJ
YgtZGOVQu2xn7zAWzU0F/OThe8oV54e1SAKcmJuDM0n5
-----END RSA PRIVATE KEY-----
```
##### 使用 RSA 私鑰去產生相對應的公鑰

[錯誤的指令]:openssl rsa -in private.pem -out public.pem -outform PEM 
```
-out" 參數指定產生的公鑰檔案名稱
"-outform" 參數指定公鑰的輸出格式==>只可以下列三種:DER/NET/PEM
openssl 預設輸入輸出的格式都是PEM
Certificate 和 key 可以存成多種格式, 常見的有 DER,PEM,PFX
不同格式轉換請參見:
http://jianiau.blogspot.com/2015/07/openssl-generating-rsa-key.html
"-pubout" 參數結尾
執行後，OpenSSL 會產生 public.pem 的檔案在磁碟中
```
cat public.pem==>答案是錯的

[正確的指令]:openssl rsa -in private.pem -out public.pem -pubout

cat public.pem 
```
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAqxBOhxtVgh0xahzTRa3A
ifJFLtBZk3LuQvWxGIE4iMdfpHF1DteyrGVhsCVOpAaFawrj1n1gWThv/BLHSYka
aJy3EzSfjAJBkqLmuncVgc4zkKPzmG/NXieT8yHEVwUDsu5/e6EgPXU52Q7sHf/L
xUfvBk5ovqVhiOxeCCH4uc39QmRVWwMBjUajTzTFvizN4fq7rctDvHjr2LWksc/K
NmlOsasGqvMyxHJSEQdOk9uTmN3EH93BIH9ZA8AE5kdUH8tUoiSbxQcv8iD2Tib1
Z4lk9dYOGjiRjkdHXYkSXZjWWvTO2hZLu82u+LaICoognEfMO42HQlVf1H8eAezf
MQIDAQAB
-----END PUBLIC KEY-----
```

[證明給我看看]使用相同的私鑰再次產生出來的金鑰還是一樣的

```
mv public.pem public2.pem
openssl rsa -in private.pem -out public.pem -outform PEM -pubout
```

```
0x01  猜解RSA私密金鑰和素因數
0x02 生成RSA私密金鑰檔
0x03 使用openssl解密RSA密文
```
### [實作4]使用 sha1對檔案進行hash[特徵|指紋]

```
openssl dgst -sha1 infile
SHA1(infile)= 4e1243bd22c66e76c2ba9eddc1f91394e57f9f83
ksu@ksu-VirtualBox:~$ cat infile
test
ksu@ksu-VirtualBox:~$ echo tesT > infile2
ksu@ksu-VirtualBox:~$ openssl dgst -sha1 infile2
SHA1(infile2)= 54d592241066bb789b069a89203eae92bf76fa74
```

## B.使用Python加密與解密

###  1.使用Python進行HASH-ing

### Python standard library
>* Python有許多內建的函式庫(可以寫成幾本書)
>* 不需安裝即可使用(第三方套件需要安裝==>Tensorflow/PyTorch)
>* 使用時請import載入相關函式庫即可

#### hashlib函式庫/套件/模組
>* hashlib是python專門提供hash演算法的函式庫，包括md5, sha1, sha224, sha256, sha384, sha512等演算法

```
>>> import hashlib
>>> m = hashlib.md5()
>>> m.update(b"Nobody inspects")
>>> m.update(b" the spammish repetition")
>>> m.digest()
    b'\\xbbd\\x9c\\x83\\xdd\\x1e\\xa5\\xc9\\xd9\\xde\\xc9\\xa1\\x8d\\xf0\\xff\\xe9'

More condensed:
>>> hashlib.sha224(b"Nobody inspects the spammish repetition").hexdigest()
```

##### Python2的範例==>作業:改成Python3
```
import hashlib

data = "I am your greatteacher"
print hashlib.md5(data).hexdigest()
print hashlib.sha1(data).hexdigest()
print hashlib.sha224(data).hexdigest()
print hashlib.sha256(data).hexdigest()
print hashlib.sha384(data).hexdigest()
print hashlib.sha512(data).hexdigest()
```

```
#!/usr/bin/python3
import hashlib
m = hashlib.md5()
data = "I am your greatteacher"

# 先將資料編碼，再更新 MD5 雜湊值
m.update(data.encode("utf-8"))

h = m.hexdigest()
print(h)
```

##### 只是小改變==>答案就會不一樣
```
import hashlib

a = "I am your greatteacher"
print hashlib.md5(a).hexdigest()

b = "I am your ggreatteacher"
print hashlib.md5(b).hexdigest()

c = "I am your Greatteacher"
print hashlib.md5(c).hexdigest()
```

##### 把你的機密檔案Hash
```
#!/usr/bin/env python

import hashlib
import sys

def main():
    if len(sys.argv) != 2:
        sys.exit('Usage: %s file' % sys.argv[0])

    filename = sys.argv[1]
    m = hashlib.md5()
    with open(filename, 'rb') as fp:
        while True:
            blk = fp.read(4096) # 4KB per block
            if not blk: break
            m.update(blk)
    print(m.hexdigest(), filename)

if __name__ == '__main__':
    main()
```
執行看看:

python3 test4.py

python3 test4.py test1.py

###  2.使用Python進行RSA非對稱式密碼加密與解密==>使用rsa模組

>* https://www.cnblogs.com/hhh5460/p/5243410.html
```
import rsa

# 生成公鑰pubkey與私鑰privkey
(pubkey, privkey) = rsa.newkeys(1024)


# 保存金鑰
with open('public.pem','w+') as f:
    f.write(pubkey.save_pkcs1().decode())

with open('private.pem','w+') as f:
    f.write(privkey.save_pkcs1().decode())


# 導入金鑰
with open('public.pem','r') as f:
    pubkey = rsa.PublicKey.load_pkcs1(f.read().encode())

with open('private.pem','r') as f:
    privkey = rsa.PrivateKey.load_pkcs1(f.read().encode())

    
# 明文
message = 'hello'

# 公開金鑰加密
crypto = rsa.encrypt(message.encode(), pubkey)

# 私密金鑰解密
message = rsa.decrypt(crypto, privkey).decode()
print(message)


# 私密金鑰簽名
signature = rsa.sign(message.encode(), privkey, 'SHA-1')

# 公開金鑰驗證
rsa.verify(message.encode(), signature, pubkey)

```
###  3.使用Python進行對稱式密碼加密與解密==>使用pycrypto模組


#### TOPICS_1:利用 Python 實作簡易 RSA 非對稱式加密法

>* https://gist.github.com/jeremy5189/8916602

```
#!/usr/bin/python
# -*- coding: utf8 -*-

# Simple RSA Implementation
# Authored by Jeremy <jeremy5189(at)gmail.com>
# Reference: http://www.ruanyifeng.com/blog/2013/07/rsa_algorithm_part_two.html

from fractions import gcd
import sys

def egcd(a, b):
    if a == 0:
        return (b, 0, 1)
    else:
        g, y, x = egcd(b % a, a)
        return (g, x - (b // a) * y, y)

def modinv(a, m):
    g, x, y = egcd(a, m)
    if g != 1:
        raise Exception('modular inverse does not exist')
    else:
        return x % m

# 選擇兩個質數以及欲加密的明文(int only)
p = 61
q = 53
messsage = 2014

# 乘積
n = p * q

# 檢查明文長度
if len(str(n)) < len(str(messsage)):
	raise Exception('message(' + str(len(str(messsage))) + \
		') 不能比 n(' + str(len(str(n))) + ') 還要長')

# 計算n的歐拉函數 φ(n)
# φ(n) = (p-1)(q-1)
phi = (p - 1) * (q - 1)

# 隨機選擇一個整數 e
# 1 < e < φ(n) AND gcd( e, φ(n) ) = 1
e = 0
for i in xrange( 2, phi ):
	if gcd( i, phi ) == 1:
		e = i
		break

# 計算 e 對於 φ(n) 的模反元素 d
# e * d mod φ(n) = 1

# 相當于二元一次方程式 ( 令 d 為 x, y 為除式之商, e, φ(n) 為常數  )
# e * x + φ(n) * y = 1

# 欲此方程式，需利用「擴展歐幾里得演算法」
# 即：給予二整數 a 、b, 必存在有整數 x 、 y 使得 ax + by = gcd(a,b)
# 今 a = e, b = φ(n) 且 gcd( e, φ(n) ) = 1
# 故符合 e * x + φ(n) * y = 1
d = modinv( e, phi );

# 金鑰產生完成，準備加密資料
# 待加密的資料只能為數字
plain = messsage

# 使用公鑰 (n,e) 加密
# pow( x, y, z ) = x^y % z
# m^e ≡ c (mod n)
cipher = pow( plain, e, n ) 

# 使用私鑰 (n,d) 解密
# c^d ≡ m (mod n)
decrypted = pow( cipher, d, n)

# 印出整個過程
print "--------- Variables ---------"
print "* p = " + str(p)
print "* q = " + str(q)
print "* n = " + str(n)
print "* phi = " + str(phi)
print "* e = " + str(e)
print "* d = " + str(d)
print "----------- Keys ------------"
print "* Public (n,e) = (" + str(n) + "," + str(e) + ")"
print "* Private (n,d) = (" + str(n) + "," + str(d) + ")"
print "* N Bit = " + str(len(bin(n)))
print "---------- Messages ---------"
print "* Plain: " + str(plain)
print "* Encrypted: " + str(cipher)
if plain == decrypted:
	print "* Decrypted: " + str(decrypted) + " (Correct)"
else:
	print "* Decrypted: " + str(decrypted) + " (Failed)"
print "----------- End -------------"
```
