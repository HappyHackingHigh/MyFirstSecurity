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

解讀關鍵組合語言(一)
>* mov
>* add、sub、imul、idiv、and、or、xor
>* inc、dec、neg、not

>* cmp
>* jmp
>* ja、jb、jna、jbe、je、jne、jz

http://www.felixcloutier.com/x86/Jcc.html


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
## 範例練習: picoCTF 2017Programmers Assemble
題目為 AT&T 格式

可參考下一頁 Intel 格式的題目

## 範例練習: Reverse CTF_read-asm

## 解讀關鍵組合語言(二)

>* push、pop



## 範例練習:picoCTF 2017_A Thing Called the Stack

## 開發組合語言(一):NASM

## 範例練習:Reverse CTF_run-asm
```
global _start

section .text
_start:
  mov rax, 1
  mov rdi, 1
  push 0x7d214e75
  push 0x525f646e
  push 0x345f6d53
  push 0x615f6531
  push 0x69706d30
  push 0x437b4654
  push 0x43747372
  push 0x6946794d //M(4d)y(79)Fi  
  mov rsi, rsp
  mov rdx, 0x40
  syscall

  mov rax, 60
  mov rdi, 0
  syscall
```

```
下載原始組合語言solve.asm
$ nasm -f elf64 solve.asm
$ ld -m elf_x86_64 -o solve solve.o
$ ./solve
```

## 開發組合語言(二):NASM

# 3.GDB 

https://henrybear327.gitbooks.io/gitbook_tutorial/content/Linux/GDB/index.html

## 範例練習: EasyCTF 2017 LuckyGuess
