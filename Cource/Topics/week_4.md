# 第四週	加密/解密與破密

課程目標:上完這課程模組後,學生要會
>* 熟悉古典密碼學的凱薩加密與解密
>* 使用線上工具完成古典密碼學的暴力破解法
>* 使用線上工具完成古典密碼學的頻率分析法
>* 熟悉古典密碼學的密碼棒之加密與解密
>* 完成crypto-CTF題目解題

延伸學習:鼓勵學生參加Breakall CTF練習

# 古典密碼學

Substitution cipher置換式密碼

## A.Substitution cipher置換式密碼

>* https://en.wikipedia.org/wiki/Substitution_cipher
>* https://zh.wikipedia.org/wiki/替換式密碼

類型

#### 簡易替換密碼（simple substitution cipher）或「單表加密」（monoalphabetic cipher）單字母替換加密

如果每一個字母為一單元（或稱元素）進行加密操作

>* Caesar cipher凱薩密碼 https://zh.wikipedia.org/wiki/凱薩密碼
>* 豬圈密碼（Pigpen cipher)亦稱共濟會密碼（masonic cipher）或共濟會員密碼（英語：Freemason's cipher）
https://en.wikipedia.org/wiki/Pigpen_cipher

#### 範例練習:Caesar cipher凱薩密碼

加密規則:針對英文字母,移位3格

Plain 明文:   ABCDEFGHIJKLMNOPQRSTUVWXYZ
Cipher密文:   XYZABCDEFGHIJKLMNOPQRSTUVW

(1)請問底下明文加密後的密文為何?
Plaintext:  THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG

(2)請你破解底下的密文!他的明文為何?

Ciphertext: QEB NRFZH YOLTK CLU GRJMP LSBO QEB IXWV ALD

#### 多表加密（polyalphabetic cipher）或「表格式加密」（polygraphic）
以數個字母為一單元


Polyalphabetic substitution


頻率分析



## B.替換式密碼

>* rail fence:籬笆式位移密碼
>*


#### 範例練習

明文:'WE ARE DISCOVERED. FLEE AT ONCE'

[1]rail fence:籬笆式位移密碼

加密方法:

(1)使用三格
(2)由上到下,再下到上將字串
W . . . E . . . C . . . R . . . L . . . T . . . E
. E . R . D . S . O . E . E . F . E . A . O . C .
. . A . . . I . . . V . . . D . . . E . . . N . .
(3)一層一層讀,第一層開始由左到右讀

==>密文: WECRL TEERD SOEEF EAOCA IVDEN

[2]Route cipher
In a route cipher, the plaintext is first written out in a grid of given dimensions, 
then read off in a pattern given in the key

W R I O R F E O E 
E E S V E L A N J 
A D C E D E T C X 

加密方法:The key might specify "spiral inwards, clockwise, starting from the top right". 

==>密文: EJXCTEDECDAEWRIORFEONALEVSE
