# PART1_程式編譯組譯與逆向(反編譯)

## c語言程式編譯與組譯
產生組語

產生AT&T語法格式的組語(gcc預設使用的格式)
```
gcc -S -masm=att XXXXX.c -o XXXXX_att.s
```
產生Intel語法格式的組語(微軟預設使用的格式)
```
gcc -S -masm=intel XXXXX.c -o XXXXX_intel.s
```
要去掉一堆註解:請加上參數-fno-asynchronous-unwind-tables
```
gcc -S -masm=intel XXXXX.c -o XXXXX_intel_OK.s -fno-asynchronous-unwind-tables
```

組譯過程

>* 將組合語言程式碼轉成機器可以執行的指令(instructions)
>* 每一個組語語句都對應一機器指令。
>* 組譯器的組譯過程相對於編譯器來講比較簡單
>* 沒有複雜的語法，也沒有語意，也不需要做指令最佳化，只是根據組語指令和機器指令的對照表一一翻譯就可以

連結過程


## JAVA程式的編譯與逆向(反編譯)

CTF實戰

## Python程式的編譯與逆向(反編譯)

## Linux 執行檔(ELF)分析

#### More Linux Binary Tools
>* objcopy
>* nm
>* addr2line:
>* strip
>* Runtime Analysis Tools:strace 
>* 
>* 
>* 

## 高階程式開發技術之函式庫(Library):靜態鏈結 vs動態鏈結[線上課程2018年底上線]

### 函式庫(Library):重用(reuse)的觀念

### 函式庫(Library)類型:Static vs Shared vs

### Linux 的 C 標準函式庫
>* https://en.wikipedia.org/wiki/C_standard_library
>* https://zh.wikipedia.org/wiki/Stdio.h

查看你linux所使用的C函式庫版本

### 靜態函式庫開發與使用

### 共享函式庫開發與使用

# PART2_x86(32位元)與x64(64位元)電腦的計算機結構

計算機組織與結構computer architecture

##### Von Neumann Architecture(1945)

##### [Memory Hierarchy記憶體階層](https://zh.wikipedia.org/wiki/記憶體階層)

##### 暫存器 registers

X86-32 internal architecture

暫存器名稱的第一個字母 E 代表 Extended，原先從 16 位元延伸到現在的 32 位元架構暫存器，故名稱上也都加上字母 E 以示別

區段暫存器 Segment registers


##### 暫存器的用途

https://arstechnica.com/gadgets/2002/03/an-introduction-to-64-bit-computing-and-x86-64/

IA-32 Memory Models(32位元的記憶體管理模式)

## 讓電腦執行運算的機械指令(machine code)

>* 機器語言Machine code|Instruction code
>* 第一代程式語言

一個資料移動的機械指令
tells an x86/IA-32 processor to move an immediate 8-bit value into a register

binary code(二進位機器碼)===>10110000 01100001

Hexadecimal十六進位表達法===>B0 61

線上反組譯服務https://www.onlinedisassembler.com/odaweb/

http://sparksandflames.com/files/x86InstructionChart.html

https://software.intel.com/en-us/articles/intel-sdm

## 從機械指令(machine code)到組合語言(Assembly code)

# 我的第一堂組合語言[線上課程2018年底上線]

### NASM:Windows 和 Linux 皆可
### MASM:Windows

Introduction to x86 Assembly Language
http://www.c-jump.com/CIS77/ASM/Assembly/index.html


# 解讀關鍵組合語言

### objdump 使用技術
```
objdump -S -M intel helloCTFer
```
去掉機器碼 --no-show-raw-insn  
```
objdump -S -j .text -M intel helloCTFer --no-show-raw-insn  
```

##### CTF實戰:Pico CTF 2014 : Function Address

### 解讀關鍵組合語言I

#### 資料定義敘述 data definition statement 

#### 記憶體資料存取:Iittle endian vs big endian 

#### 資料轉移Data Transfers

x86 指令格式


### 解讀關鍵組合語言II:Function Call and Calling conventions

#### 堆疊 Stack及其運算


https://en.wikipedia.org/wiki/X86_calling_conventions#List_of_x86_calling_conventions

Function prologues函數頭
https://en.wikipedia.org/wiki/Function_prologue

function epilogues函數尾

# gdb技術與實戰CTF

### 強化你的gdb之PEDA
>* [PEDA - Python Exploit Development Assistance for GDB](https://github.com/longld/peda)
>* 為GDB設計的一個強大的外掛程式
>* 提供了很多人性化的功能，比如高亮顯示反彙編代碼、寄存器、記憶體資訊，提高了debug的效率。
>* PEDA還為GDB添加了一些實用新的命令，比如checksec可以查看程式開啟了哪些安全機制等等

##### 安裝PEDA
```
git clone https://github.com/longld/peda.git ~/peda
echo "source ~/peda/peda.py" >> ~/.gdbinit
```
##### 使用PEDA

### 強化你的gdb之pwndbg[略]
>* [pwndbg](https://github.com/pwndbg/pwndbg)

# IDA pro技術與實戰CTF

# 逆向工程
>* http://reversing.kr/
>* https://beginners.re/
>* https://github.com/dennis714/RE-for-beginners
>* https://challenges.re/


# NEXT(加入資安實務導師培訓制度學習更多技術)

### [Windows PE/PE+執行檔分析](https://en.wikipedia.org/wiki/Portable_Executable)

### radara 2技術與實戰:從reversing 到 PWN
>* https://github.com/radare/radare2

### Z3技術與實戰

### Angr技術與實戰







