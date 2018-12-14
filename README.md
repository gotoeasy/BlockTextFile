# `缘起`
在各种项目的开发过程中，不断的使用着各种配置文件，ini、properties、xml、json、yaml等等<br>
简而言之，各有千秋，但却总有挠不到的痒处

作为一种给人读的文本文件，需要简单明了，且又不失灵活<br>
最终，自创发明了 `Block-Text-File` 格式文件，实际使用后可谓得心应手，大有用途，绝非仅限于配置

鉴于应用效果优良，现整理发布，以飨同仁

<br>
青松 2018年8月25日
<br>
<br>

### `块文本文件说明书`
以下是块文本文件（`Block-Text-File`文件，简称BTF文件）的格式定义说明书　`欢迎转载，但请勿改动定义以免混淆误解`

[![Version](https://img.shields.io/badge/Version-1.1.0-blue.svg)](https://github.com/gotoeasy/block-text-file) 
[![License](https://img.shields.io/badge/License-Apache%202-brightgreen.svg)](https://github.com/gotoeasy/block-text-file/blob/master/LICENSE)
<br>
<br>

#### 文件编码
* 文件编码固定为 `UTF-8`

#### 格式定义
* BTF文件由0~N个文档`Document`构成，`Document`之间的分隔行由9个等号`=========`开始，转义时首位为`\`
* 一个`Document`由0~N个块`Block-Text`构成，`Block-Text`可以指定`块结束行`，`块结束行`由9个减号`---------`开始，转义时首位为`\`
* 一个块由`块名行`和`块内容`组成，`块名行`由`块名`开始，`块名`用中括号`[]`包围，次行开始到块结束之间的文本为`块内容`，`块名`含`]`时用`\]`转义
* `块名`不区分大小写，`块内容`的最后一个换行符（\r\n或\n）将被忽视
* 其他无关的内容将被忽视，可作适当作注释用途使用
<br>
<br>

### `Sample`
下面是个一目了然的例子<br>
其中有properties、json甚至template等各种形式的内容，灵活性凸显，就看你怎么驾驭使用了
```
sample.btf
[properties]
key1=value1
key2=value2
key3=value3

[sampledata]
{
"id": code-1",
"name": "ABCD",
"price": 123
}

[template]
NNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNN
NNNNNNNNNNNNNNNNN
```
<br>

再写个注解的例子，以直观的理解BTF文件格式定义
```
从这行开始，到[aaa]块名行之间的内容是被忽视的，可写注释用

[aaa] 这行是【块名行】，块名是aaa，忽略大小写，在块名结束后的字符都被忽视，可写注释用
A1 这是块aaa的文本内容行，A1行、A2行、A3行都是，最后一个换行符(\r\n或\n)在A3行的行末，将被忽视
A2 这是块aaa的文本内容行，A1行、A2行、A3行都是，最后一个换行符(\r\n或\n)在A3行的行末，将被忽视
A3 这是块aaa的文本内容行，A1行、A2行、A3行都是，最后一个换行符(\r\n或\n)在A3行的行末，将被忽视
---------------------------------这行由9个减号开始，是【块结束行】，9个减号后的字符被忽视，可写注释用
这里到[bbb]块名行之间的内容也是被忽视的，可写注释用

 [xxx]这行也是被忽视的，虽然看起来像是块名行，但这行实际是由一个空格开始，所以不是块名行
 
 
[bbb]  BTF格式文件的主要特点就是块名易懂、同时不限制块内容格式交由用户自定义使用
NNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNN


============ 这行是9个等号开始的【文档分隔行】，9个等号后的字符被忽视，可写注释用，多文档组合功能可进一步满足扩展的需求

[conf]
aaa = xxxxxx
bbb = xxxxxx
ccc = xxxxxx
```
<br>

### `链接`
* `@gotoeasy/btf` [![NPM version](https://img.shields.io/npm/v/@gotoeasy/btf.svg)](https://www.npmjs.com/package/@gotoeasy/btf) https://github.com/gotoeasy/npm-packages/blob/master/btf

<br>
<br>

<hr>

### `变更列表`
[![Version](https://img.shields.io/badge/Version-1.1.0-blue.svg)](https://github.com/gotoeasy/block-text-file/blob/master/version1.1.0.md) <br>
添加字符串转义功能
* 块名转义 `[\]]` => 块名为`]`，注：最后一个右中括号不做转义，`[\]` => 块名为`\`，`[\]\]` => 块名为`]\`<br>
* 块结束行转义 `\----------` => 按块内容处理转换为`---------`<br>
* 文档分隔行转义 `\=========` => 按块内容处理转换为`=========`<br>
<br>

[![Version](https://img.shields.io/badge/Version-1.0.0-blue.svg)](https://github.com/gotoeasy/block-text-file/blob/master/version1.0.0.md) <br>
完成基本格式定义
