# c語言程式編譯組譯與與逆向

# c語言程式編譯組譯

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

# c程式執行檔逆向==>逆向成組合語言

# c程式執行檔逆向==>逆向成C語言


