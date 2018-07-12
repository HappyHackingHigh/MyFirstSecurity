#第七週	現代密碼加密與解密

課程目標:上完這課程模組後,學生要會

>* 了解對稱式密碼與非對稱式密碼的觀念
>* 熟悉使用openssl進行DES對稱式密碼的加密與解密
>* 熟悉使用openssl進行RSA非對稱式密碼的加密與解密
>* 熟悉使用openssl進行MD/SHA1/SHA2562雜湊的應用
>* 熟悉使用Python進行RSA非對稱式密碼的加密與解密[選擇性]

# openssl
>* https://zh.wikipedia.org/wiki/OpenSSL


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
