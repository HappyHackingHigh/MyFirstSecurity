# 第七週	現代密碼加解密與破密

進階主題: 基礎RSA破密分析[選擇性]

>* Twin Prime的RSA破密分析
>* common factor attack
>* 加密指數攻擊:Hastad’s Broadcast Attack
>* 模數攻擊:common modulus attack

# python第三方工具安裝

## python 破密分析工具

#### pycrypto::Python Cryptography Toolkit 

>* https://pypi.org/project/pycrypto/

This is a collection of both secure hash functions (such as SHA256 and RIPEMD160), and various encryption algorithms (AES, DES, RSA, ElGamal, etc.). 

The package is structured to make adding new modules easy. This section is essentially complete, and the software interface will almost certainly not change in an incompatible way in the future; all that remains to be done is to fix any bugs that show up. 

#### sympy::Python library for symbolic mathematics

>* http://www.sympy.org/en/index.html
>* http://docs.sympy.org/latest/tutorial/preliminaries.html  線上試試看

SymPy is a Python library for symbolic mathematics. 

It aims to become a full-featured computer algebra system (CAS) while keeping the code as simple as possible in order to be comprehensible and easily extensible. SymPy is written entirely in Python.

The SymPy CAS can be installed on virtually any computer with Python 2.7 or above. SymPy does require mpmath Python library to be installed first. The recommended method of installation is through Anaconda, which includes mpmath, as well as several other useful libraries. Alternatively, some Linux distributions have SymPy packages available.

SymPy officially supports Python 2.7, 3.4, 3.5, 3.6 and PyPy.


$ python
```
>>> from sympy import *
>> x = Symbol('x')
>>> limit(sin(x)/x, x, 0)
1
>>> integrate(1/x, x)
log(x)
>>> a = Integral(cos(x)*exp(x), x)
>>> Eq(a, a.doit())

看看你還記得微積分的積分技術嗎?

```


#### python-gmpy::General MultiPrecision arithmetic for Python

gmpy is a C-coded Python extension module that provides access to the GMP (or MPIR) multiple-precision arithmetic library.

GMPY allows creation of multiprecision integer (mpz), float (mpf),and rational (mpq) numbers, 
conversion between them and to/from Python numbers/strings, arithmetic, bitwise, 
and some other higher-level mathematical operations.

>* https://github.com/aleaxit/gmpy

gmpy2 is an optimized, C-coded Python extension module that supports fast
multiple-precision arithmetic.  gmpy2 is based on the original gmpy module.
gmpy2 adds support for correctly rounded multiple-precision real arithmetic
(using the MPFR library) and complex arithmetic (using the MPC library).

>* 說明文件 https://gmpy2.readthedocs.io/en/latest/

```
>>> import gmpy2
>>> from gmpy2 import mpz
>>> mpz('123') + 1
mpz(124)
>>> 10 - mpz(1)
mpz(9)
>>> gmpy2.is_prime(17)
True
```

#### rsa
>* https://stuvel.eu/rsa   有許多說明文件
>* https://pypi.org/project/rsa/
>* https://github.com/sybrenstuvel/python-rsa/

use the rsa.newkeys() function to create a keypair:
```
>>> import rsa
>>> (pubkey, privkey) = rsa.newkeys(512)
```

use rsa.PrivateKey.load_pkcs1() and rsa.PublicKey.load_pkcs1() to load keys from a file:
```
>>> import rsa
>>> with open('private.pem', mode='rb') as privatefile:
...     keydata = privatefile.read()
>>> privkey = rsa.PrivateKey.load_pkcs1(keydata)
```

5.3. Encryption and decryption¶

To encrypt or decrypt a message, use rsa.encrypt() resp. rsa.decrypt().

Let’s say that Alice wants to send a message that only Bob can read.

Bob generates a keypair, and gives the public key to Alice. 
This is done such that Alice knows for sure that the key is really Bob’s 
(for example by handing over a USB stick that contains the key).
```
>>> import rsa
>>> (bob_pub, bob_priv) = rsa.newkeys(512)
```
Alice writes a message, and encodes it in UTF-8. 
The RSA module only operates on bytes, and not on strings, so this step is necessary.
```
>>> message = 'hello Bob!'.encode('utf8')
```
Alice encrypts the message using Bob’s public key, and sends the encrypted message.
```
>>> import rsa
>>> crypto = rsa.encrypt(message, bob_pub)
```
Bob receives the message, and decrypts it with his private key.
```
>>> message = rsa.decrypt(crypto, bob_priv)
>>> print(message.decode('utf8'))
hello Bob!
```
Since Bob kept his private key private, Alice can be sure that he is the only one who can read the message. Bob does not know for sure that it was Alice that sent the message, since she didn’t sign it.

RSA can only encrypt messages that are smaller than the key. A couple of bytes are lost on random padding, and the rest is available for the message itself. For example, a 512-bit key can encode a 53-byte message (512 bit = 64 bytes, 11 bytes are used for random padding and other stuff). See Working with big files for information on how to work with larger files.

Altering the encrypted information will likely cause a rsa.pkcs1.DecryptionError. If you want to be sure, use rsa.sign().
```
>>> crypto = rsa.encrypt(b'hello', bob_pub)
>>> crypto = crypto[:-1] + b'X' # change the last byte
>>> rsa.decrypt(crypto, bob_priv)
Traceback (most recent call last):
...
rsa.pkcs1.DecryptionError: Decryption failed
```

#### RSAtool
>* RSAtool是一個非常方便實用的小工具，可以用來計算RSA中的幾個參數、生成金鑰、加解密，一些不太複雜的破解工作也可以用它。
>* https://github.com/ius/rsatool

#### libnum
>* https://github.com/hellman/libnum
>* Requirements: python2.7

# 運作在Python 2環境的工具

### 
```
sudo apt-get install python-pip
sudo apt-get install libgmp-dev
sudo pip install --upgrade setuptools

sudo pip install pycrypto
sudo pip install sympy
sudo apt-get install python-gmpy2
sudo pip install rsa
```
### 安裝libnum
```
git clone https://github.com/hellman/libnum
cd libnum
sudo python setup.py install
```
# 運作在Python 3環境的工具

### 
```
sudo apt-get install python3-pip
sudo pip3 install --upgrade setuptools

sudo pip3 install pycrypto
sudo pip3 install sympy
sudo apt-get install python3-gmpy2
sudo pip3 install rsa
```
### 安裝rsatool
```
git clone https://github.com/ius/rsatool
cd rsatool
sudo python setup.py install
```
### 安裝HashPump
```
git clone https://github.com/bwall/HashPump.git
sudo apt-get install g++ libssl-dev
cd HashPump
make
sudo make install
```

### 安裝rsa-wiener-attack工具

>* https://en.wikipedia.org/wiki/Wiener%27s_attack
>* https://github.com/pablocelayes/rsa-wiener-attack

A Python implementation of the Wiener attack on RSA public-key encryption scheme.

It uses some results about continued fractions approximations to infer the private key from public key 
in the cases the encryption exponent is too small or too large.
```
git clone https://github.com/pablocelayes/rsa-wiener-attack
cd rsa-wiener-attack

```
### 安裝yafu

>* https://github.com/DarkenCode/yafu
>* https://sourceforge.net/projects/yafu/

```
wget https://jaist.dl.sourceforge.net/project/yafu/1.34/yafu-1.34.zip
unzip yafu-1.34.zip -d yafu
cd yafu
chmod +x yafu
```


