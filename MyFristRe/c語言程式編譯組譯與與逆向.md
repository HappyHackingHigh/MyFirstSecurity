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

![組合語言](pic/b.png)

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
使用xxd看看object file的內容==>xxd hello.o
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
```
objdump -S -M intel helloCTF
```

```
helloCTF:     file format elf64-x86-64


Disassembly of section .init:

00000000004003c8 <_init>:
  4003c8:	48 83 ec 08          	sub    rsp,0x8
  4003cc:	48 8b 05 25 0c 20 00 	mov    rax,QWORD PTR [rip+0x200c25]        # 600ff8 <_DYNAMIC+0x1d0>
  4003d3:	48 85 c0             	test   rax,rax
  4003d6:	74 05                	je     4003dd <_init+0x15>
  4003d8:	e8 43 00 00 00       	call   400420 <__libc_start_main@plt+0x10>
  4003dd:	48 83 c4 08          	add    rsp,0x8
  4003e1:	c3                   	ret    

Disassembly of section .plt:

00000000004003f0 <puts@plt-0x10>:
  4003f0:	ff 35 12 0c 20 00    	push   QWORD PTR [rip+0x200c12]        # 601008 <_GLOBAL_OFFSET_TABLE_+0x8>
  4003f6:	ff 25 14 0c 20 00    	jmp    QWORD PTR [rip+0x200c14]        # 601010 <_GLOBAL_OFFSET_TABLE_+0x10>
  4003fc:	0f 1f 40 00          	nop    DWORD PTR [rax+0x0]

0000000000400400 <puts@plt>:
  400400:	ff 25 12 0c 20 00    	jmp    QWORD PTR [rip+0x200c12]        # 601018 <_GLOBAL_OFFSET_TABLE_+0x18>
  400406:	68 00 00 00 00       	push   0x0
  40040b:	e9 e0 ff ff ff       	jmp    4003f0 <_init+0x28>

0000000000400410 <__libc_start_main@plt>:
  400410:	ff 25 0a 0c 20 00    	jmp    QWORD PTR [rip+0x200c0a]        # 601020 <_GLOBAL_OFFSET_TABLE_+0x20>
  400416:	68 01 00 00 00       	push   0x1
  40041b:	e9 d0 ff ff ff       	jmp    4003f0 <_init+0x28>

Disassembly of section .plt.got:

0000000000400420 <.plt.got>:
  400420:	ff 25 d2 0b 20 00    	jmp    QWORD PTR [rip+0x200bd2]        # 600ff8 <_DYNAMIC+0x1d0>
  400426:	66 90                	xchg   ax,ax

Disassembly of section .text:

0000000000400430 <_start>:
  400430:	31 ed                	xor    ebp,ebp
  400432:	49 89 d1             	mov    r9,rdx
  400435:	5e                   	pop    rsi
  400436:	48 89 e2             	mov    rdx,rsp
  400439:	48 83 e4 f0          	and    rsp,0xfffffffffffffff0
  40043d:	50                   	push   rax
  40043e:	54                   	push   rsp
  40043f:	49 c7 c0 b0 05 40 00 	mov    r8,0x4005b0
  400446:	48 c7 c1 40 05 40 00 	mov    rcx,0x400540
  40044d:	48 c7 c7 26 05 40 00 	mov    rdi,0x400526
  400454:	e8 b7 ff ff ff       	call   400410 <__libc_start_main@plt>
  400459:	f4                   	hlt    
  40045a:	66 0f 1f 44 00 00    	nop    WORD PTR [rax+rax*1+0x0]

0000000000400460 <deregister_tm_clones>:
  400460:	b8 3f 10 60 00       	mov    eax,0x60103f
  400465:	55                   	push   rbp
  400466:	48 2d 38 10 60 00    	sub    rax,0x601038
  40046c:	48 83 f8 0e          	cmp    rax,0xe
  400470:	48 89 e5             	mov    rbp,rsp
  400473:	76 1b                	jbe    400490 <deregister_tm_clones+0x30>
  400475:	b8 00 00 00 00       	mov    eax,0x0
  40047a:	48 85 c0             	test   rax,rax
  40047d:	74 11                	je     400490 <deregister_tm_clones+0x30>
  40047f:	5d                   	pop    rbp
  400480:	bf 38 10 60 00       	mov    edi,0x601038
  400485:	ff e0                	jmp    rax
  400487:	66 0f 1f 84 00 00 00 	nop    WORD PTR [rax+rax*1+0x0]
  40048e:	00 00 
  400490:	5d                   	pop    rbp
  400491:	c3                   	ret    
  400492:	0f 1f 40 00          	nop    DWORD PTR [rax+0x0]
  400496:	66 2e 0f 1f 84 00 00 	nop    WORD PTR cs:[rax+rax*1+0x0]
  40049d:	00 00 00 

00000000004004a0 <register_tm_clones>:
  4004a0:	be 38 10 60 00       	mov    esi,0x601038
  4004a5:	55                   	push   rbp
  4004a6:	48 81 ee 38 10 60 00 	sub    rsi,0x601038
  4004ad:	48 c1 fe 03          	sar    rsi,0x3
  4004b1:	48 89 e5             	mov    rbp,rsp
  4004b4:	48 89 f0             	mov    rax,rsi
  4004b7:	48 c1 e8 3f          	shr    rax,0x3f
  4004bb:	48 01 c6             	add    rsi,rax
  4004be:	48 d1 fe             	sar    rsi,1
  4004c1:	74 15                	je     4004d8 <register_tm_clones+0x38>
  4004c3:	b8 00 00 00 00       	mov    eax,0x0
  4004c8:	48 85 c0             	test   rax,rax
  4004cb:	74 0b                	je     4004d8 <register_tm_clones+0x38>
  4004cd:	5d                   	pop    rbp
  4004ce:	bf 38 10 60 00       	mov    edi,0x601038
  4004d3:	ff e0                	jmp    rax
  4004d5:	0f 1f 00             	nop    DWORD PTR [rax]
  4004d8:	5d                   	pop    rbp
  4004d9:	c3                   	ret    
  4004da:	66 0f 1f 44 00 00    	nop    WORD PTR [rax+rax*1+0x0]

00000000004004e0 <__do_global_dtors_aux>:
  4004e0:	80 3d 51 0b 20 00 00 	cmp    BYTE PTR [rip+0x200b51],0x0        # 601038 <__TMC_END__>
  4004e7:	75 11                	jne    4004fa <__do_global_dtors_aux+0x1a>
  4004e9:	55                   	push   rbp
  4004ea:	48 89 e5             	mov    rbp,rsp
  4004ed:	e8 6e ff ff ff       	call   400460 <deregister_tm_clones>
  4004f2:	5d                   	pop    rbp
  4004f3:	c6 05 3e 0b 20 00 01 	mov    BYTE PTR [rip+0x200b3e],0x1        # 601038 <__TMC_END__>
  4004fa:	f3 c3                	repz ret 
  4004fc:	0f 1f 40 00          	nop    DWORD PTR [rax+0x0]

0000000000400500 <frame_dummy>:
  400500:	bf 20 0e 60 00       	mov    edi,0x600e20
  400505:	48 83 3f 00          	cmp    QWORD PTR [rdi],0x0
  400509:	75 05                	jne    400510 <frame_dummy+0x10>
  40050b:	eb 93                	jmp    4004a0 <register_tm_clones>
  40050d:	0f 1f 00             	nop    DWORD PTR [rax]
  400510:	b8 00 00 00 00       	mov    eax,0x0
  400515:	48 85 c0             	test   rax,rax
  400518:	74 f1                	je     40050b <frame_dummy+0xb>
  40051a:	55                   	push   rbp
  40051b:	48 89 e5             	mov    rbp,rsp
  40051e:	ff d0                	call   rax
  400520:	5d                   	pop    rbp
  400521:	e9 7a ff ff ff       	jmp    4004a0 <register_tm_clones>

0000000000400526 <main>:
  400526:	55                   	push   rbp
  400527:	48 89 e5             	mov    rbp,rsp
  40052a:	bf c4 05 40 00       	mov    edi,0x4005c4
  40052f:	e8 cc fe ff ff       	call   400400 <puts@plt>
  400534:	b8 00 00 00 00       	mov    eax,0x0
  400539:	5d                   	pop    rbp
  40053a:	c3                   	ret    
  40053b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000400540 <__libc_csu_init>:
  400540:	41 57                	push   r15
  400542:	41 56                	push   r14
  400544:	41 89 ff             	mov    r15d,edi
  400547:	41 55                	push   r13
  400549:	41 54                	push   r12
  40054b:	4c 8d 25 be 08 20 00 	lea    r12,[rip+0x2008be]        # 600e10 <__frame_dummy_init_array_entry>
  400552:	55                   	push   rbp
  400553:	48 8d 2d be 08 20 00 	lea    rbp,[rip+0x2008be]        # 600e18 <__init_array_end>
  40055a:	53                   	push   rbx
  40055b:	49 89 f6             	mov    r14,rsi
  40055e:	49 89 d5             	mov    r13,rdx
  400561:	4c 29 e5             	sub    rbp,r12
  400564:	48 83 ec 08          	sub    rsp,0x8
  400568:	48 c1 fd 03          	sar    rbp,0x3
  40056c:	e8 57 fe ff ff       	call   4003c8 <_init>
  400571:	48 85 ed             	test   rbp,rbp
  400574:	74 20                	je     400596 <__libc_csu_init+0x56>
  400576:	31 db                	xor    ebx,ebx
  400578:	0f 1f 84 00 00 00 00 	nop    DWORD PTR [rax+rax*1+0x0]
  40057f:	00 
  400580:	4c 89 ea             	mov    rdx,r13
  400583:	4c 89 f6             	mov    rsi,r14
  400586:	44 89 ff             	mov    edi,r15d
  400589:	41 ff 14 dc          	call   QWORD PTR [r12+rbx*8]
  40058d:	48 83 c3 01          	add    rbx,0x1
  400591:	48 39 eb             	cmp    rbx,rbp
  400594:	75 ea                	jne    400580 <__libc_csu_init+0x40>
  400596:	48 83 c4 08          	add    rsp,0x8
  40059a:	5b                   	pop    rbx
  40059b:	5d                   	pop    rbp
  40059c:	41 5c                	pop    r12
  40059e:	41 5d                	pop    r13
  4005a0:	41 5e                	pop    r14
  4005a2:	41 5f                	pop    r15
  4005a4:	c3                   	ret    
  4005a5:	90                   	nop
  4005a6:	66 2e 0f 1f 84 00 00 	nop    WORD PTR cs:[rax+rax*1+0x0]
  4005ad:	00 00 00 

00000000004005b0 <__libc_csu_fini>:
  4005b0:	f3 c3                	repz ret 

Disassembly of section .fini:

00000000004005b4 <_fini>:
  4005b4:	48 83 ec 08          	sub    rsp,0x8
  4005b8:	48 83 c4 08          	add    rsp,0x8
  4005bc:	c3                   	ret    


```


# c程式執行檔逆向==>逆向成C語言

# 作業

把上述的作業練習在Raspberry Pi 3在做一次

Raspberry Pi 3上安裝Ubuntu MATE作業系統

ARM 的組合語言和x86/x64的組合語言不同


