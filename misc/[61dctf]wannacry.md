## 描述

dky是干嘛的呢大家可以查一查

[wa.7z.62e898c914027fc5500d94896005a1ce](./assets/wa.7z.62e898c914027fc5500d94896005a1ce)

## 题解

单独查一下 `dky` 查不到啥，查 `wncry` 查到了勒索病毒的东西？？所以给的两个文件我猜是被勒索病毒加密了的文件和 key。

两个关键词同时搜，搜到了一个 repo：https://github.com/gentilkiwi/wanakiwi

解勒索病毒的 :) 但是在这里应该是没必要用的（因为我试了下，这玩意是生成 00000000.dky 的，而这个我们已经有了）

网上搜了一下这个 wannacry 勒索病毒，找到份报告，感觉挺有意思的

https://www.antiy.com/response/wannacry.html

看到

> 样本自身存在一个主RSA公钥1，攻击者保留主RSA私钥1。在加密文件之前首先生成一对RSA子密钥对，分别为子公钥和子私钥，随后样本对子私钥使用主RSA公钥1进行加密保存为“00000000.eky”，然后将子公钥保存为“00000000.pky”做后续使用。随后样本生成用于加密文件的AES密钥，对文件进行加密，加密后的文件内容为M2，同时使用“00000000.pky”加密AES密钥并与文件大小等数据生成M1，随后将M1、M2合并并添加“WANACRY!”文件头保存文件加密文件。在解密文件时，攻击者将“00000000.eky”解密，样本收到解密文件后将其保存为“00000000.dky”用于解密文件。样本自身还存在一对主RSA公钥、私钥对，用于解密演示文件。具体加密解密流程图如下：

简单的 RSA + AES 加密 :) 这个勒索病毒的加密手段简单粗暴易懂，不过的确有效无解

找到了一份代码，可以直接解密：

https://github.com/gentilkiwi/wanadecrypt

编译以后执行

```
$wanadecrypt.exe 00000000.dky e6a27149a1f8223e99ede949172051cd.jpg.WNCRY
```

即可得到图片，flag 在图片上面。

## 答案

flag{C0N6r475_Y0U_8347_W4NN4CrY_4641N_29cc2df9}
