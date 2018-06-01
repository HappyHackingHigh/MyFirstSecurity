# [組合語言(Assembly language)](https://en.wikipedia.org/wiki/Assembly_language)

維基百科
>* 低階語言
>* 在不同的裝置中，組合語言對應著不同的[機器語言指令集(machine instruction set)](https://en.wikipedia.org/wiki/Instruction_set_architecture)。
>* 一種組合語言專用於某種電腦系統結構
>* 
>* 組譯過程:使用組合語言編寫的原始碼，然後通過相應的組譯程式(assembler)將它們轉換成可執行的機器碼。
>* 組合語言使用助憶碼（Mnemonics）來代替和表示特定低階機器語言的操作。
>* 特定的組譯目標指令集可能會包括特定的運算元。
>* http://www.duntemann.com/assembly.html

### ARM Instruction Set
>* [ARM架構](https://zh.wikipedia.org/wiki/ARM%E6%9E%B6%E6%A7%8B)
>* a family of reduced instruction set computing (RISC) architectures for computer processors,
>* 
>* 
>* Raspberry Pi 3 Model B ARMv8（含1GB RAM）
>* ARM體系結構與編程(第2版) ARM体系结构与编程(第2版) 杜春雷 清華大學出版社 出版日期:2015-08-01

### x86/amd64組譯指令的兩大風格
>* complex instruction set computing (CISC)

### 指令(instruction)

![指令(instruction)](pic/instruction.png)

### [Intel x86 組合語言與組譯器(assembler)](https://en.wikipedia.org/wiki/Comparison_of_assemblers)

>* MASM(Microsoft Macro Assembler)
>* [NASM(Netwide Assembler)](https://en.wikipedia.org/wiki/Netwide_Assembler)
>* Flat Assembler (FASM) 
>* GNU Assembler (GAS) 
>* High Level Assembly (HLA) 
>* Turbo Assembler (TASM) 
>* Open Watcom Assembler (WASM) 
>* [Yasm](https://en.wikipedia.org/wiki/Yasm)

### Id常用指令

# NASM組合語言程式

### NASM組合語言程式範例

目的:小寫轉成大寫
程式名稱:uppercaser2.asm
參考資料:
測試步驟:

nasm -f elf -g -F stabs uppercaser2.asm;    

ld -o uppercaser2 uppercaser2.o

echo asdmvd > test.txt

./uppercaser2 >test_upper.txt < test.txt

cat test_upper.txt 


程式名稱:hexdump.asm
參考資料:CH9

測試步驟:

gedit hexdump1.asm

nasm -f elf -g -F stabs hexdump1.asm

ld -o hexdump1 hexdump1.o

./hexdump1 < /bin/ls



 
