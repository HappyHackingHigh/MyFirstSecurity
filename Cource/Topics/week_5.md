# Crypto_101_凱薩密碼擴充版

>* RC3 CTF 2016 : salad-100
>* https://github.com/ctfs/write-ups-2016/tree/master/rc3-ctf-2016/crypto/salad-100
>* https://github.com/ctfs/write-ups-2016/tree/master/rc3-ctf-2016/crypto/salad-100
>* 使用python程式解題
```
import string

caesaralpha = "abcdefghijklmnopqrstuvwxyz0123456789"

def caesar(input_string, rot):
    output_string = ""
    for i in range(len(input_string)):
        if input_string[i].isalnum():
            idx = (caesaralpha.find(input_string[i]) + rot) % len(caesaralpha)
            output_string += caesaralpha[idx]
        else:
            output_string += input_string[i]
    return output_string

enc = '7sj-ighm-742q3w4t' # encrypt data

for i in range(len(caesaralpha)):
    print caesar(enc, i)
```

# Transposition cipher

https://en.wikipedia.org/wiki/Transposition_cipher




# Crypto_102_Transposition cipher

>*  AlexCTF2017: Fore1-Hit_the_core 50
>*  https://isitdtu.blogspot.tw/2017/02/alexctf-2017-fore1-hit-core-forensics-50.html

解題步驟1:
```
file fore1.core 
```
解題步驟2:

$ strings fore1.core
```
….
cvqAeqacLtqazEigwiXobxrCrtuiTzahfFreqc{bnjrKwgk83kgd43j85ePgb_e_rwqr7fvbmHjklo3tews_hmkogooyf0vbnk0ii87Drfgh_n kiwutfb0ghk9ro987k5tfb_hjiouo087ptfcv}
….
```

解題步驟3:使用python解題

sol

```
cipher='cvqAeqacLtqazEigwiXobxrCrtuiTzahfFreqc{bnjrKwgk83kgd43j85ePgb_e_rwqr7fvbmHjklo3tews_hmkogooyf0vbnk0ii87Drfgh_n kiwutfb0ghk9ro987k5tfb_hjiouo087ptfcv}'

cipher=cipher[3:]
flag = ''
for x in range(0,len(cipher),1):
    if x%5==0:
        flag+=cipher[x]
print flag

```

```
cipher='cvqAeqacLtqazEigwiXobxrCrtuiTzahfFreqc{bnjrKwgk83kgd43j85ePgb_e_rwqr7fvbmHjklo3tews_hmkogooyf0vbnk0ii87Drfgh_n kiwutfb0ghk9ro987k5tfb_hjiouo087ptfcv}'

''.join(cipher[3 : : 5])
```

```
s = 'cvqAeqacLtqazEigwiXobxrCrtuiTzahfFreqc{bnjrKwgk83kgd43j85ePgb_e_rwqr7fvbmHjklo3tews_hmkogooyf0vbnk0ii87Drfgh_n kiwutfb0ghk9ro987k5tfb_hjiouo087ptfcv}'
print s[3::5]
```

python sol.py


# Crypto_103_affine-cipher

>*  School CTF 2015: affine-cipher-100(教) 150
>*  https://github.com/BurningMarshmallow/CTF/blob/master/affine_solve.py

解題:使用python程式解題

```
import string

s = string.ascii_lowercase # a-z
s += '_'
d = {}
for c in range(len(s)):
	d[s[(c*4 + 15)%27]] = s[c]
ciphertext = 'ifpmluglesecdlqp_rclfrseljpkq'
s1 = ''
for x in cr:
	s1 += d[x]
print s1
```

