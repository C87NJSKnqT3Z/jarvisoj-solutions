## 描述

没想到RSA4096都被你给破了，一定是我的问题，给了你太多信息，这次我只给你一个flag的加密值和公钥，仍然是RSA4096，我就不信你还能解出来。

[extremelyhardRSA.rar.8782e822c895a2af3d8ba4ffbb3e280b](./assets/extremelyhardRSA.rar.8782e822c895a2af3d8ba4ffbb3e280b)

## 题解

先看看公钥里的信息

```
$ RsaCtfTool.py --dumpkey --key pubkey.pem 
[*] n: 721059527572145959497866070657244746540818298735241721382435892767279354577831824618770455583435147844630635953460258329387406192598509097375098935299515255208445013180388186216473913754107215551156731413550416051385656895153798495423962750773689964815342291306243827028882267935999927349370340823239030087548468521168519725061290069094595524921012137038227208900579645041589141405674545883465785472925889948455146449614776287566375730215127615312001651111977914327170496695481547965108836595145998046638495232893568434202438172004892803105333017726958632541897741726563336871452837359564555756166187509015523771005760534037559648199915268764998183410394036820824721644946933656264441126738697663216138624571035323231711566263476403936148535644088575960271071967700560360448191493328793704136810376879662623765917690163480410089565377528947433177653458111431603202302962218312038109342064899388130688144810901340648989107010954279327738671710906115976561154622625847780945535284376248111949506936128229494332806622251145622565895781480383025403043645862516504771643210000415216199272423542871886181906457361118669629044165861299560814450960273479900717138570739601887771447529543568822851100841225147694940195217298482866496536787241
[*] e: 3
```

显然这是一个中国剩余定理的题，直接用工具解就好。详细原理见 

https://ctf-wiki.github.io/ctf-wiki/crypto/asymmetric/rsa/rsa_e_attack-zh/#_1

咱就使用这个命令就好

```
$ RsaCtfTool.py --publickey pubkey.pem --uncipherfile flag.enc --attack hastads
[+] Clear text : b"Didn't you know RSA padding is really important? Now you see a non-padding message is so dangerous. And you should notice this in future.Fl4g: PCTF{Sm4ll_3xpon3nt_i5_W3ak}\n"
```

好像等了一个小时左右。。。才破解出来

## 答案

PCTF{Sm4ll_3xpon3nt_i5_W3ak}