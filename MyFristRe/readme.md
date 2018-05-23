

# x86(32位元)與x64(64位元)電腦的計算機結構

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

## 從機械指令(machine code)到組合語言(Assembly code)

# 我的第一堂組合語言

### NASM:Windows 和 Linux 皆可
### MASM:Windows


# 解讀關鍵組合語言

### objdump 使用技術

objdump -S -M intel helloCTFer

去掉機器碼 --no-show-raw-insn  

objdump -S -j .text -M intel helloCTFer --no-show-raw-insn  
 


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





