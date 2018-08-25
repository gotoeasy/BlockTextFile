# `缘起`
在各种项目的开发过程中，不断的使用着各种配置文件，ini、properties、xml、json、yaml等等<br>
简而言之，各有千秋，却总有挠不到的痒处

作为一种给人读的文本文件，需要简单明了，且又不失灵活<br>
最终，自创发明Block-Text-File格式文件，实际使用后可谓得心应手，大有用途，绝非仅限于配置

鉴于应用效果优良，现整理发布，以飨同行


### `块文本文件说明书`
以下是块文本文件（Block-Text-File文件，简称BTF文件）的格式定义说明书，`欢迎转载，但请勿改动以免发生误解`

#### 文件编码
* 文件编码，固定为UTF-8

#### 格式定义
* BTF文件由0~N个文档Document构成，Document之间的分隔行由9个等号`=========`开始
* 一个Document由0~N个块Block-Text构成，Block-Text可以指定块结束行，块结束行由9个减号`---------`开始
* 一个块由块名行和块内容组成，块名行由块名开始，块名用中括号`[]`包围，次行开始到块结束之间的文本为块内容
* 块名不区分大小写，块内容的最后一个换行符（\r\n或\n）将被忽视
* 其他无关的内容将被忽视，同时可作注释用途使用
<br>

### `Sample`
```
[properties]
key1=value1
key2=value2
key3=value3

[jsondata]
{
"id": code-1",
"name": "ABCD",
"price": 123
}

[mail-template]
NNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNN
NNNNNNNNNNNNNNNNN
---------

[ftpserver]
ip = 192.168.11.22
username = N*&*^jvu^%#@$@#%$&*&^^*%^&
password = @#%$YD%&##@$#$!#*&%^%$%^$%

=========这行是9个等号开始的【文档分隔行】，9个等号后的字符被忽视，可写注释用
从这行开始，到[aaa]块名行之间的内容是被忽视的，可写注释用

[aaa] 这行是【块名行】，在块名结束后的字符都被忽视，可写注释用
NNNNNNNNNNNNNNNN
MMMMMMMMMMMMMMMMMMMMMM
XXXXXXXXXX
NNNNNNNNNNNNNNNNNNNN
---------这行是9个减号开始的【块结束行】，9个减号后的字符被忽视，可写注释用
这里到[bbb]块名行之间的内容也是被忽视的，可写注释用


[bbb]
NNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNN
=======================

[conf1]
aaa = xxxxxx
bbb = xxxxxx
ccc = xxxxxx

[conf2]
aaa = xxxxxx
bbb = xxxxxx
ccc = xxxxxx

[conf3]
aaa = xxxxxx
bbb = xxxxxx
ccc = xxxxxx

```
