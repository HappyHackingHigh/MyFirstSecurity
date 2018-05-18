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

編譯階段==>gcc –S XXX.i  –o XXX.s

組譯階段==>gcc –c XXX.s –o XXX.o

連結階段==>gcc  XXX.o –o XXX
