## Bitwise Operators

|操作符|名称|语法|计算规则|
|---|---|---|---|
|&|AND|a & b|对应位都为1时结果为1，否则为0|
|\||OR|a \| b|对应位有一个为1时结果为1，否则为0|
|^|XOR|a ^ b|对应位不同则结果为1，相同则为0|
|~|NOT|~a|将每个位取反|
|<<|左移|a << n|将a的所有位向左移动n位，右边补0|
|>>|右移|a >> n|将a的所有位向右移动n位，左边补0|
左右对齐优先级小于乘除
## IPv4地址是整数

我们需要把输入的字符，转换成整数

```c
unsigned int a1 = 192;
unsigned int a2 = 168;
unsigned int a3 = 1;
unsigned int a4 = 3;
//转换为三十二位数的前八位
```
过程解释：
a1 192 1100,0000 -> 1100,0000,0000,0000,0000,0000,0000,0000 a1 = a1<<3\*8
a2 168 1010,1000 -> 0000,0000,1010,1000,0000,0000,0000,0000 a2 = a2<<2\*8
a3 1     0000,0001 -> 0000,0000,0000,0000,0000,0001,0000,0000  
a4 3     0000,0011 -> 

整数是一位一位等着被运算的空间，你可以通过位移之类的bitwise operations来操作他们，得到想要的结果。

## BASE64 编码器

BASE64 需求

无损 
有规则

记事本是一次性load进内存的，而其它的不大一样，是分段读取的

初步设计
Base64 Algorithm 
    Problem:
        128 ASCII characters, only 95 ASCII characters are Readable
        There are also some characters not allowed (,.%:...)
        The number of characters are less than 1 Byte is required
    Solution:
        建立索引
        1 character
        那我怎么知道它补零了呢？
        编码的时候，正常情况下，是一个整数是四位数。如果这个四位数只有三位，后面是0，还好。如果不是0？那就会有空余。
        等号，额外的编码位会变成等号。