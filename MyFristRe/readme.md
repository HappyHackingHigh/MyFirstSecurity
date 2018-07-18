# MyFirstReversing上課平台

### 000題庫--linux基本指令

### 100題庫--組合語言

### 200題庫--GDB使用技術

### 300題庫--JAVA逆向技術

### 400題庫--Python逆向技術

### 500題庫-unpacking/deobfuscation

### 600題庫-Angr/Z3使用技術

### windows題庫--windows使用技術(reversing.kr)


# Reversing-CTF平台

#!/usr/bin/env python3
import binascii
key = "graAhogG"
data = "6513c2b1c2bac3835f0cc28a5b6ac2abc2b9c2bfc381c39b7613c3bac2b3c2a17f7ac29f00c3aa46c2b9c2a6"
def mystery(s):
    r = ""
    tran = binascii.unhexlify(data).decode("utf-8")
    for i, c in enumerate(tran):
        r += chr(ord(c) ^ ((i * ord(key[i % len(key)])) % 256))
    return bytes(r, "utf-8")
 
print(mystery(data))
