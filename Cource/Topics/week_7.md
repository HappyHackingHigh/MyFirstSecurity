# 第七週	現代密碼加密與解密

課程目標:上完這課程模組後,學生要會

>* 了解對稱式密碼與非對稱式密碼的觀念
>* 熟悉使用openssl進行DES對稱式密碼的加密與解密
>* 熟悉使用openssl進行RSA非對稱式密碼的加密與解密
>* 熟悉使用openssl進行MD/SHA1/SHA2562雜湊的應用
>* 熟悉使用Python進行RSA非對稱式密碼的加密與解密[選擇性]

# openssl
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
#### [實作2] 使用 DES 加密與解密

##### 使用 DES 加密

ksu@ksu-VirtualBox:~$ echo test > infile

ksu@ksu-VirtualBox:~$ cat infile

openssl des -in infile -out infile.des
```
執行後，OpenSSL 會提示使用者由鍵盤上輸入加密之密碼，如下:
    enter des-cbc encryption password:
不管鍵盤輸入什麼，畫面上都不會出現任何字元。輸入完成後，按下鍵盤上的 "Enter" 鍵即可。

OpenSSL 會再一次要求使用者輸入一次相同的密碼
加密的檔案將以 file.des 的名稱存在於磁碟中。
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

#### [實作3] 使用 3DES 加密與解密

>* 只要把上述的des改成des3

##### 使用 Triple DES加密
```
openssl des3 -in myfile -out file.des3
```
##### 使用 Triple DES解密
```
openssl des3 -d -in file.des3 -out HIfile
```

### 資料加密標準DES::Data Encryption Standard

>* https://zh.wikipedia.org/wiki/資料加密標準


### 三重DES(Triple-DES)

>* https://zh.wikipedia.org/wiki/三重資料加密演算法


#### [實作3] 使用 3DES 加密與解密

#### [實作3] 使用 sha1對檔案進行hash[特徵|指紋]
openssl dgst -sha1 infile
SHA1(infile)= 4e1243bd22c66e76c2ba9eddc1f91394e57f9f83
ksu@ksu-VirtualBox:~$ cat infile
test
ksu@ksu-VirtualBox:~$ echo tesT > infile2
ksu@ksu-VirtualBox:~$ openssl dgst -sha1 infile2
SHA1(infile2)= 54d592241066bb789b069a89203eae92bf76fa74

# 使用Python加密與解密

###  熟悉使用Python進行RSA非對稱式密碼加密與解密==>使用rsa模組

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


### 利用 Python 實作簡易 RSA 非對稱式加密法

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
