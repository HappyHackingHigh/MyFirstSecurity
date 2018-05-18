C程式の編譯
```
#include <stdio.h>

int main()
{
    int a=5;
    //printf("input integer number: ");
    //scanf("%d",&a);
    switch(a)
    {
        case 1:printf("Monday\n");printf("BreakallCTF{Can you see me wahahahahaha}\n");
        break;
        case 2:printf("Tuesday\n");
        break;
        case 3:printf("Wednesday\n");
        break;
        case 4:printf("Thursday\n");
        break;
        case 5:printf("Friday\n");
        break;
        case 6:printf("Saturday\n");
        break;
        case 7:printf("Sunday\n");
        break;
        default:printf("error\n");
    }
}
```
預處理階段==>gcc –E XXX.c –o XXX.i

```
# 1 "test.c"
# 1 "<built-in>"
# 1 "<command-line>"
# 1 "/usr/include/stdc-predef.h" 1 3 4
# 1 "<command-line>" 2
# 1 "test.c"
# 1 "/usr/include/stdio.h" 1 3 4
# 27 "/usr/include/stdio.h" 3 4
# 1 "/usr/include/features.h" 1 3 4
# 367 "/usr/include/features.h" 3 4
# 1 "/usr/include/x86_64-linux-gnu/sys/cdefs.h" 1 3 4
# 410 "/usr/include/x86_64-linux-gnu/sys/cdefs.h" 3 4
# 1 "/usr/include/x86_64-linux-gnu/bits/wordsize.h" 1 3 4
# 411 "/usr/include/x86_64-linux-gnu/sys/cdefs.h" 2 3 4
# 368 "/usr/include/features.h" 2 3 4
# 391 "/usr/include/features.h" 3 4
# 1 "/usr/include/x86_64-linux-gnu/gnu/stubs.h" 1 3 4
# 10 "/usr/include/x86_64-linux-gnu/gnu/stubs.h" 3 4
# 1 "/usr/include/x86_64-linux-gnu/gnu/stubs-64.h" 1 3 4
# 11 "/usr/include/x86_64-linux-gnu/gnu/stubs.h" 2 3 4
# 392 "/usr/include/features.h" 2 3 4
# 28 "/usr/include/stdio.h" 2 3 4





# 1 "/usr/lib/gcc/x86_64-linux-gnu/5/include/stddef.h" 1 3 4
# 216 "/usr/lib/gcc/x86_64-linux-gnu/5/include/stddef.h" 3 4


# 2 "test.c" 2


# 3 "test.c"
int main()
{
    int a=5;


    switch(a)
    {
        case 1:printf("Monday\n");printf("BreakallCTF{Can you see me wahahahahaha}\n");
        break;
        case 2:printf("Tuesday\n");
        break;
        case 3:printf("Wednesday\n");
        break;
        case 4:printf("Thursday\n");
        break;
        case 5:printf("Friday\n");
        break;
        case 6:printf("Saturday\n");
        break;
        case 7:printf("Sunday\n");
        break;
        default:printf("error\n");
    }
}
```

編譯階段==>gcc –S XXX.i  –o XXX.s

file test.s

test.s: assembler source, ASCII text
```
	.file	"test.c"
	.section	.rodata
.LC0:
	.string	"Monday"
	.align 8
.LC1:
	.string	"BreakallCTF{Can you see me wahahahahaha}"
.LC2:
	.string	"Tuesday"
.LC3:
	.string	"Wednesday"
.LC4:
	.string	"Thursday"
.LC5:
	.string	"Friday"
.LC6:
	.string	"Saturday"
.LC7:
	.string	"Sunday"
.LC8:
	.string	"error"
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
	subq	$16, %rsp
	movl	$5, -4(%rbp)
	cmpl	$7, -4(%rbp)
	ja	.L2
	movl	-4(%rbp), %eax
	movq	.L4(,%rax,8), %rax
	jmp	*%rax
	.section	.rodata
	.align 8
	.align 4
.L4:
	.quad	.L2
	.quad	.L3
	.quad	.L5
	.quad	.L6
	.quad	.L7
	.quad	.L8
	.quad	.L9
	.quad	.L10
	.text
.L3:
	movl	$.LC0, %edi
	call	puts
	movl	$.LC1, %edi
	call	puts
	jmp	.L11
.L5:
	movl	$.LC2, %edi
	call	puts
	jmp	.L11
.L6:
	movl	$.LC3, %edi
	call	puts
	jmp	.L11
.L7:
	movl	$.LC4, %edi
	call	puts
	jmp	.L11
.L8:
	movl	$.LC5, %edi
	call	puts
	jmp	.L11
.L9:
	movl	$.LC6, %edi
	call	puts
	jmp	.L11
.L10:
	movl	$.LC7, %edi
	call	puts
	jmp	.L11
.L2:
	movl	$.LC8, %edi
	call	puts
.L11:
	movl	$0, %eax
	leave
	.cfi_def_cfa 7, 8
	ret
	.cfi_endproc
.LFE0:
	.size	main, .-main
	.ident	"GCC: (Ubuntu 5.4.0-6ubuntu1~16.04.5) 5.4.0 20160609"
	.section	.note.GNU-stack,"",@progbits
```
組譯階段==>gcc –c XXX.s –o XXX.o

```
test.o: ELF 64-bit LSB relocatable, x86-64, version 1 (SYSV), not stripped
```

xxd test.o

連結階段==>gcc  XXX.o –o XXX
