# gdb

# gdb執行
方法1:執行 binary 並且使用 gdb 來 debug===>$ gdb <binary>

方法2:先執行 gdb 之後再 attach 上要 debug 的 process
```
$ gdb
attach <pid>
```

# GDB 基本指令

開啟要被debug的檔案 (如果你用gdb (執行檔檔名) 啟動 GDB 的話，這個file指令就不必做了)

file (用 -g 參數編譯的執行檔檔名) 例如：file hw1.exe

執行要被debug的程式 (下過這個指令後，debug程序才正式展開! 這就像是你用./去執行一個程式一樣的意思。)

注意! 沒有設定breakpoint的話，程式會一直執行到結束喔!! Breakpoint的目的就是要debugger在特定地方停下來!

run ===> 可用縮寫 r ===>執行下一行指令，function call會被當作一行指令，不會進去function裡面一行一行執行

next ===> 可用縮寫 n ===>執行下一道指令

連function都會進去一行一行執行 ==> step

看某變數的數值 ==>  print (變數名) 或 p (變數名)

設置 breakpoint (建議 run 之前就先設定好基本的breakpoint) ===> break (行數) 或 b (行數)

在每一次的 next/step 後, 都要顯示出數值的變數  ===>  display (變數名)

看看目前display, breakpoint等等的設定狀態 ===> info break/display/...

看看 source code ===>  list

看所有register的數值(直接輸入 info 可以查詢指令) ===> info all-registers

開啟內建說明 ===> help

# gdb 常用指令--範例示範

http://www.study-area.org/goldencat/debug.htm


# gdb 演練

# gdb 常用指令--參考資料
