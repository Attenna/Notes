十六进制数字，16位计算机内存地址：
	AF 01
	需要注意，
		二进制：
			64 32 16 8 4 2 1
			 1   1   1  1 1 1 1
		 十六进制：
			 1 2 3 4 5 6 7 8 9 10  A   B   C   D   E   F
			 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16
	因此，16位内存地址的数量级在2^16
	转换成十六进制，16 == 2^4
	所以，16/4 == 4，十六进制下的内存地址就应该有四个数码位。

C语言是一种：
	高级语言（High-Level Language）
	编译型语言（Compiled Language）
	面向过程语言（Structured Language）

以下是C语言应用程序创建过程的是（Programming steps to create an executable C program）：
	编写（Edit）
	编译（Compile）
	链接（Link）（内存交流）

ASCII如下
	![[Pasted image 20241112235821.png]]
	A从65开始
	a从97开始
	0从48开始
	null == 0
	\r内码取值是13
	“空格”是32

编写Hello World：
```c
#include <stdio.h>
	int main(){
		printf("Hello World!");
		return 0;
	}
```

计算周长：
```c
#include <stdio.h>
	int main(){
		const double PI = 3.1416;
		double r = 10;
		double c = 2*PI*r;
		printf("%5.2f\n",c);
		return 0;
	}
```
其中，%5.2f\n是用作格式化的，5表示最小宽度，不满5个字符的就用空格补，\n是换行。


### 数据类型
int
	[signed] short int i;
	short int i;
	[signed] int i;
	int i;
	[signed] long int i;
float

数据类型尺寸——*sizeof()*
取值范围
二进制单位——比特位,bit,b
内存机构的最小寻址单位——字节，byte
	1 byte = 8bit
0 = 0 = 0
11111111 = 255 = FF
size of int
1 = 1
11 = 3
111 = 7
1111 = 15
11111 = 63

signed 符号位，如果是0，则证，1，则负。
三十二位的数，除去左边第一个符号位，剩下的位数只有三十一
_补码_
	正数的补码是数的二进制形式
	负数是绝对值数码取反，再加一
