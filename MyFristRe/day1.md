https://github.com/ss8651twtw/CTF/tree/master/site/csie.ctf.tw/practice


https://tlk.io/reverse


# tmux

sudo apt install tmux

tmux

# week_1

Topic_1_Basic tools

Topic_2_Assembly Language

Topic_3_gdb


# 1.Basic tools

>* file and strings
>* lstrace and strace
>* objdump
>* packing and unpacking


## Basic tools---file and strings


## 範例練習:EasyCTF IV_hexedit

https://github.com/mohamedaymenkarmous/CTF/blob/master/EasyCTF_IV/resources/reverse_engineering-50-hexedit

## 範例練習:EasyCTF 2017_ Hexable

https://github.com/easyctf/easyctf-2017-problems/blob/master/hexable-autogen/description.md

## Basic tools---strace

## 範例練習:strace

```
wget 'https://github.com/ss8651twtw/CTF/tree/master/site/csie.ctf.tw/practice/strace'
chmod +x strace
./strace
strace ./strace
strace -s 40 ./strace
```
## Basic tools---objdump

## 範例練習:
```
objdump -M intel -d ./search | grep -A 2 'mov BYTE PTR [rip+0x.*],0x4d' | grep 0x79

取出關鍵欄位 ==> cat out | awk '{print $8}'

hex to string ==> http://www.convertstring.com/zh_TW/EncodeDecode/HexDecode
```
# 2.Assembly Language

## 範例練習:picoCTF 2017_A Thing Called the Stack

## 範例練習:

# 3.GDB 

## 範例練習: EasyCTF 2017 LuckyGuess
