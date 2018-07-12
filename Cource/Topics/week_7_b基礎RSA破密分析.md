# 第七週	現代密碼加解密與破密

進階主題: 基礎RSA破密分析[選擇性]

>* Twin Prime的RSA破密分析
>* common factor attack
>* 加密指數攻擊:Hastad’s Broadcast Attack
>* 模數攻擊:common modulus attack

# python第三方工具安裝

## python 破密分析工具

pycrypto

sympy

python-gmpy

rsa

https://github.com/ius/rsatool

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

