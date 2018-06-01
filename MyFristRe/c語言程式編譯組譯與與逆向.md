# c語言程式編譯組譯與與逆向

# c語言程式編譯組譯

c語言程式:hello.c
```
#include <stdio.h>

int x=5;

int main()
{
   printf("Hello CTFer\n ”);
   return 0;
}

```
【推薦好書】程式設計師的自我修養：連結、載入、程式庫

## 預處理階段

```
gcc –E XXX.c –o XXX.i
```

查看.i的架構==>hello.i
```

```

## 編譯階段:產生組語
```
gcc –S XXX.i  –o XXX.s
```

產生的組合語言(assembly)

>* 預設是AT&T組合語言格式
```
	.file	"hello.c"
	.section	.rodata
.LC0:
	.string	"Hello CTFer"
	.text
	.globl	main
	.type	main, @function
main:
.LFB0:
	.cfi_startproc
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset 6, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register 6
	movl	$.LC0, %edi
	call	puts
	movl	$0, %eax
	popq	%rbp
	.cfi_def_cfa 7, 8
	ret
	.cfi_endproc
.LFE0:
	.size	main, .-main
	.ident	"GCC: (Ubuntu 5.4.0-6ubuntu1~16.04.5) 5.4.0 20160609"
	.section	.note.GNU-stack,"",@progbits
```

#### 產生AT&T語法格式的組語(gcc預設使用的格式)
```
gcc -S -masm=att XXXXX.c -o XXXXX_att.s
```
```
	.file	"hello.c"
	.section	.rodata
.LC0:
	.string	"Hello CTFer"
	.text
	.globl	main
	.type	main, @function
main:
.LFB0:
	.cfi_startproc
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset 6, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register 6
	movl	$.LC0, %edi
	call	puts
	movl	$0, %eax
	popq	%rbp
	.cfi_def_cfa 7, 8
	ret
	.cfi_endproc
.LFE0:
	.size	main, .-main
	.ident	"GCC: (Ubuntu 5.4.0-6ubuntu1~16.04.5) 5.4.0 20160609"
	.section	.note.GNU-stack,"",@progbits
```
#### 產生Intel語法格式的組語(微軟預設使用的格式)
```
gcc -S -masm=intel XXXXX.c -o XXXXX_intel.s
```

```
	.file	"hello.c"
	.intel_syntax noprefix
	.section	.rodata
.LC0:
	.string	"Hello CTFer"
	.text
	.globl	main
	.type	main, @function
main:
.LFB0:
	.cfi_startproc
	push	rbp
	.cfi_def_cfa_offset 16
	.cfi_offset 6, -16
	mov	rbp, rsp
	.cfi_def_cfa_register 6
	mov	edi, OFFSET FLAT:.LC0
	call	puts
	mov	eax, 0
	pop	rbp
	.cfi_def_cfa 7, 8
	ret
	.cfi_endproc
.LFE0:
	.size	main, .-main
	.ident	"GCC: (Ubuntu 5.4.0-6ubuntu1~16.04.5) 5.4.0 20160609"
	.section	.note.GNU-stack,"",@progbits
```

![組合語言](/pic/a.png)

#### 要去掉一堆註解:請加上參數-fno-asynchronous-unwind-tables
```
gcc -S -masm=intel XXXXX.c -o XXXXX_intel_OK.s -fno-asynchronous-unwind-tables
```
```
	.file	"hello.c"
	.intel_syntax noprefix
	.section	.rodata
.LC0:
	.string	"Hello CTFer"
	.text
	.globl	main
	.type	main, @function
main:
	push	rbp
	mov	rbp, rsp
	mov	edi, OFFSET FLAT:.LC0
	call	puts
	mov	eax, 0
	pop	rbp
	ret
	.size	main, .-main
	.ident	"GCC: (Ubuntu 5.4.0-6ubuntu1~16.04.5) 5.4.0 20160609"
	.section	.note.GNU-stack,"",@progbits
```
## 組譯過程

>* 將組合語言程式碼轉成機器可以執行的指令(instructions)
>* 每一個組語語句都對應一機器指令。
>* 組譯器的組譯過程相對於編譯器來講比較簡單
>* 沒有複雜的語法，也沒有語意，也不需要做指令最佳化，只是根據組語指令和機器指令的對照表一一翻譯就可以
```
gcc –c XXX.s –o XXX.o
```
使用xxd看看onject file的內容==>xxd hello.o
```
00000000: 7f45 4c46 0201 0100 0000 0000 0000 0000  .ELF............
00000010: 0100 3e00 0100 0000 0000 0000 0000 0000  ..>.............
00000020: 0000 0000 0000 0000 a002 0000 0000 0000  ................
00000030: 0000 0000 4000 0000 0000 4000 0d00 0a00  ....@.....@.....
00000040: 5548 89e5 bf00 0000 00e8 0000 0000 b800  UH..............
00000050: 0000 005d c348 656c 6c6f 2043 5446 6572  ...].Hello CTFer
00000060: 0000 4743 433a 2028 5562 756e 7475 2035  ..GCC: (Ubuntu 5
00000070: 2e34 2e30 2d36 7562 756e 7475 317e 3136  .4.0-6ubuntu1~16
00000080: 2e30 342e 3529 2035 2e34 2e30 2032 3031  .04.5) 5.4.0 201
00000090: 3630 3630 3900 0000 1400 0000 0000 0000  60609...........
000000a0: 017a 5200 0178 1001 1b0c 0708 9001 0000  .zR..x..........
000000b0: 1c00 0000 1c00 0000 0000 0000 1500 0000  ................
000000c0: 0041 0e10 8602 430d 0650 0c07 0800 0000  .A....C..P......
000000d0: 0000 0000 0000 0000 0000 0000 0000 0000  ................
000000e0: 0000 0000 0000 0000 0100 0000 0400 f1ff  ................
000000f0: 0000 0000 0000 0000 0000 0000 0000 0000  ................

```
## 連結過程
```
gcc  XXX.o –o XXX
```
```
gcc  XXX.o –o XXX.exe
```

```
gcc  XXX.o –o XXX.jpg
```

看看不同階段產生的檔案大小:
```
-rw-rw-r-- 1 ksu ksu    76  六   1 08:27 hello.c
-rw-rw-r-- 1 ksu ksu 17106  六   1 08:27 hello.i
-rwxrwxr-x 1 ksu ksu  8600  六   1 08:56 hello.jpg
-rw-rw-r-- 1 ksu ksu  1504  六   1 09:00 hello.o
-rw-rw-r-- 1 ksu ksu   455  六   1 08:50 hello.s
```
# c程式執行檔逆向==>逆向成組合語言

# c程式執行檔逆向==>逆向成C語言


