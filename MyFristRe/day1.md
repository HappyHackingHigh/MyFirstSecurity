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

## 範例練習:組合語言的解讀

```
.global main

main:
    mov eax, XXXXXXX
    mov ebx, 0
    mov ecx, 0x5
    
loop:
    test eax, eax
    jz fin
    add ebx, ecx
    dec eax
    jmp loop
    
fin:
    cmp ebx, 0x7ee0
    je good
    mov eax, 0
    jmp end
good:
    mov eax, 1
end:
    ret
```

```
eax = xxxxxxx
ebx = 0
ecx = 5


while (eax != 0) {
	ebx += ecx
	eax--
}

if (ebx == 0x7ee0) {
	// good
	eax = 1
	return
}
else {
	eax = 0
	return
}

```
## 範例練習:picoCTF 2017_A Thing Called the Stack

## 範例練習: picoCTF 2017Programmers Assemble
題目為 AT&T 格式

可參考下一頁 Intel 格式的題目

## 範例練習: Reverse CTF_read-asm

# 3.GDB 

## 範例練習: EasyCTF 2017 LuckyGuess
