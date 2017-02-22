> 参考《鸟哥的Linux私房菜》

# 基础

`grep [-acinv] [--color=auto] '搜索字符串' filename`

- -a：将 binary 档案以 text 档案的方式搜寻数据
- -c：计算找到 '搜寻字符串' 的次数
- -i：忽略大小写的不同，所以大小写视为相同
- -n：顺便输出行号
- -v：反向选择，亦即显示出没有 '搜寻字符串' 内容的那一行
- --color=auto：可以将找到的关键词部分加上颜色的显示

## 例子

- `grep -n 'the' filename.log`  
  在 filename.log 文件中搜寻 'the' 字符串，并输出行号

# 进阶

`grep [-A] [-B] [--color=auto] '搜寻字符串' filename`

- -A：后面可加数字，为 after 的意思，除了列出该行外，后续的 n 行也列出来
- -B：后面可加数字，为 before 的意思，除了列出该行外，前面的 n 行也列出来

## 例子

- `dmesg | grep -n -A3 -B2 'eth'`  
  用 dmesg 列出核心讯息，再以 grep 找出内含 eth 的行，在关键词所在行的前两行与后三行也一起提出来显示

# grep 结合正则表达式

- `grep -n 't[ae]st' filename.log`  
  在 filename.log 文件中搜寻 test 或 tast 这两个单字

- `grep -n '[^g]oo' filename.log`  
  在 filename.log 文件中搜寻 oo 字符串，并且 oo 前面不能是 g

- `grep -n '^the' filename.log`  
  在 filename.log 文件中搜寻 the 字符串，并且 the 字符串出现在行首

- `grep -n '^$' filename.log`  
  在 filename.log 文件中搜寻空行

- `grep -n 'o\{2\}' filename.log`  
  在 filename.log 文件中搜寻含有 oo（即两个o） 字符串的行

- `grep -n 'o\{2,5\}' filename.log`  
  在 filename.log 文件中搜寻含有 2 到 5 个连续 o 字符的行
  
- `grep -n 'o\{2,}' filename.log`  
  在 filename.log 文件中搜寻含有 2 个或 2 个以上连续 o 字符的行
