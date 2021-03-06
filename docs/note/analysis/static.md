# 静态分析

# IDA Pro

## 求余数运算反汇编

求余运算F5反汇编结果如下：

```C
v5 = 3 * v0 - 0X30 * ((unsigned __int64)(0xAAAAAAAAAAAAAAABLL * (unsigned __int128)(3 * v0) >> 64) >> 5);
```

其实相当于如下运算：

```C
v5 = 3 * v0 % 0x30;
```

# Ghidra


# radare2 常用指令

## r2
### hex文件编辑
 - `V` -> 图形化界面: 
  - `c` -> 选字节编辑; 
   ```
   $ r2 -w ./xxx #打开写文件权限后可编辑文件
   ```
  - `i` -> 编辑字节;
  - `p` -> 切换模式;

### print
 - pd - 反汇编
 - ps - 字符串
 - px - 16进制(4bytes)
 - pxw - (8bytes)

## rabin2
 - `$ rabin2 -zz ./file` -> dump全部字符串
 - `-M` -> main addr
 - `-i` -> Imports (PLT)
 - `-E` -> Export
 - `-s` -> Symbols
 - `-S` -> Sections (text, plt, bss, dynsym...)
 - `-R` -> Relocations (GOT)
 - `-H` -> ELF Header信息
 - `-l` -> Linked libraries

## rax2
```
% rax2 -h
Usage: rax2 [options] [expr ...]
  =[base]                      ;  rax2 =10 0x46 -> output in base 10
  int     ->  hex              ;  rax2 10
  hex     ->  int              ;  rax2 0xa
  -int    ->  hex              ;  rax2 -77
  -hex    ->  int              ;  rax2 0xffffffb3
  int     ->  bin              ;  rax2 b30
  int     ->  ternary          ;  rax2 t42
  bin     ->  int              ;  rax2 1010d
  ternary ->  int              ;  rax2 1010dt
  float   ->  hex              ;  rax2 3.33f
  hex     ->  float            ;  rax2 Fx40551ed8
  oct     ->  hex              ;  rax2 35o
  hex     ->  oct              ;  rax2 Ox12 (O is a letter)
  bin     ->  hex              ;  rax2 1100011b
  hex     ->  bin              ;  rax2 Bx63
  ternary ->  hex              ;  rax2 212t
  hex     ->  ternary          ;  rax2 Tx23
  raw     ->  hex              ;  rax2 -S < /binfile
  hex     ->  raw              ;  rax2 -s 414141
  -l                           ;  append newline to output (for -E/-D/-r/..
  -a      show ascii table     ;  rax2 -a
  -b      bin -> str           ;  rax2 -b 01000101 01110110
  -B      str -> bin           ;  rax2 -B hello
  -d      force integer        ;  rax2 -d 3 -> 3 instead of 0x3
  -e      swap endianness      ;  rax2 -e 0x33
  -D      base64 decode        ;
  -E      base64 encode        ;
  -f      floating point       ;  rax2 -f 6.3+2.1
  -F      stdin slurp code hex ;  rax2 -F < shellcode.[c/py/js]
  -h      help                 ;  rax2 -h
  -i      dump as C byte array ;  rax2 -i < bytes
  -k      keep base            ;  rax2 -k 33+3 -> 36
  -K      randomart            ;  rax2 -K 0x34 1020304050
  -L      bin -> hex(bignum)   ;  rax2 -L 111111111 # 0x1ff
  -n      binary number        ;  rax2 -n 0x1234 # 34120000
  -o      octalstr -> raw      ;  rax2 -o \162 \62 # r2
  -N      binary number        ;  rax2 -N 0x1234 # \x34\x12\x00\x00
  -r      r2 style output      ;  rax2 -r 0x1234
  -s      hexstr -> raw        ;  rax2 -s 43 4a 50
  -S      raw -> hexstr        ;  rax2 -S < /bin/ls > ls.hex
  -t      tstamp -> str        ;  rax2 -t 1234567890
  -x      hash string          ;  rax2 -x linux osx
  -u      units                ;  rax2 -u 389289238 # 317.0M
  -w      signed word          ;  rax2 -w 16 0xffff
  -v      version              ;  rax2 -v
```