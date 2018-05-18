C程式の編譯

預處理階段==>gcc –E XXX.c –o XXX.i

編譯階段==>gcc –S XXX.i  –o XXX.s

組譯階段==>gcc –c XXX.s –o XXX.o

連結階段==>gcc  XXX.o –o XXX
