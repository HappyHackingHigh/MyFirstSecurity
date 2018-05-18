# JAVA編譯與反編譯
>* 編譯==>javac xxx.java  ==> 產生xxx.class
>* 執行==>java xxx

# JAVA反編譯==>jad


```
Jad v1.5.8e. Copyright 2001 Pavel Kouznetsov (kpdus@yahoo.com).
Usage:    jad [option(s)] <filename(s)>
Options: -a       - generate JVM instructions as comments (annotate)
         -af      - output fully qualified names when annotating
         -b       - generate redundant braces (braces)
         -clear   - clear all prefixes, including the default ones
         -d <dir> - directory for output files
         -dead    - try to decompile dead parts of code (if there are any)
         -dis     - disassembler only (disassembler)
         -f       - generate fully qualified names (fullnames)
         -ff      - output fields before methods (fieldsfirst)
         -i       - print default initializers for fields (definits)
         -l<num>  - split strings into pieces of max <num> chars (splitstr)
         -lnc     - output original line numbers as comments (lnc)
         -lradix<num>- display long integers using the specified radix
         -nl      - split strings on newline characters (splitstr)
         -noconv  - don't convert Java identifiers into valid ones (noconv)
         -nocast  - don't generate auxiliary casts
         -noclass - don't convert .class operators
         -nocode  - don't generate the source code for methods
         -noctor  - suppress the empty constructors
         -nodos   - turn off check for class files written in DOS mode
         -nofd    - don't disambiguate fields with the same names (nofldis)
         -noinner - turn off the support of inner classes
         -nolvt   - ignore Local Variable Table entries (nolvt)
         -nonlb   - don't insert a newline before opening brace (nonlb)
         -o       - overwrite output files without confirmation
         -p       - send all output to STDOUT (for piping)
         -pa <pfx>- prefix for all packages in generated source files
         -pc <pfx>- prefix for classes with numerical names (default: _cls)
         -pe <pfx>- prefix for unused exception names (default: _ex)
         -pf <pfx>- prefix for fields with numerical names (default: _fld)
         -pi<num> - pack imports into one line using .* (packimports)
         -pl <pfx>- prefix for locals with numerical names (default: _lcl)
         -pm <pfx>- prefix for methods with numerical names (default: _mth)
         -pp <pfx>- prefix for method parms with numerical names (default:_prm)
         -pv<num> - pack fields with the same types into one line (packfields)
         -r       - restore package directory structure
         -radix<num>- display integers using the specified radix (8, 10, or 16)
         -s <ext> - output file extension (default: .jad)
         -safe    - generate additional casts to disambiguate methods/fields
         -space   - output space between keyword (if, while, etc) and expression
         -stat    - show the total number of processed classes/methods/fields
         -t<num>  - use <num> spaces for indentation (default: 4)
         -t       - use tabs instead of spaces for indentation
         -v       - show method names while decompiling
```

jad abc.class 
Parsing abc.class...The class file version is 52.0 (only 45.3, 46.0 and 47.0 are supported)
 Generating abc.jad

```
// Decompiled by Jad v1.5.8e. Copyright 2001 Pavel Kouznetsov.
// Jad home page: http://www.geocities.com/kpdus/jad.html
// Decompiler options: packimports(3) 
// Source File Name:   abc.java

import java.io.PrintStream;

public class abc
{

    public abc()
    {
    }

    public static void main(String args[])
    {
        char ac[] = {
            'r', 'u', 'n', 'o', 'o', 'b'
        };
        String s = new String(ac);
        System.out.println(s);
    }
}

```
```
cat Authenticator.jad 
// Decompiled by Jad v1.5.8e. Copyright 2001 Pavel Kouznetsov.
// Jad home page: http://www.geocities.com/kpdus/jad.html
// Decompiler options: packimports(3) 
// Source File Name:   Authenticator.java

import java.io.Console;
import java.io.PrintStream;

class Authenticator
{

    public Authenticator()
    {
    }

    public static void main(String args[])
    {
        key = new char[10];
        key[0] = 'A';
        key[1] = 'o';
        key[2] = 'J';
        key[3] = 'k';
        key[4] = 'V';
        key[5] = 'h';
        key[6] = 'L';
        key[7] = 'w';
        key[8] = 'U';
        key[9] = 'R';
        Console console = System.console();
        for(String s = ""; !s.equals("ThisIsth3mag1calString4458"); 
            s = console.readLine("Enter password:", new Object[0]));
        for(int i = 0; i < key.length; i++)
            System.out.print(key[i]);

        System.out.println("");
    }

    public static char key[];
}
```
