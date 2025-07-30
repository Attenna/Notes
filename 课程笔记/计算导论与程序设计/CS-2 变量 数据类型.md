下面符合变量命名规则的是：
	name
	\_name
	name\_
	name4
	myName
	my\_name

下面属于整形的是：
	int
	long
	long long

执行下面代码，本题目用作熟悉格式化操作符。
	```
```c
#include <stdio.h>

int main()
{
   printf ("Characters: %c, %c \n", 'a', 65);
     printf ("Characters: %c, %c \n", 'A'+1, 65+1);
   printf ("Decimals: %d, %ld\n", 'A', 650000L);
   printf ("Preceding with blanks: %10d \n", 1977);
   printf ("Preceding with zeros  : %010d \n", 1977);
   printf ("Some different radices: %d, %x, %o, %#x, %#o \n", 100, 100, 100, 100, 100);
   printf ("Floats: %4.2f, %+.0e, %E \n", 3.1416, 3.1416, 3.1416);
   printf ("Width trick: %*d \n", 5, 10);
   printf (String: "%s \n", "A string");
   return 0;
}
```
a A B B 65 650000 1977 0000001977 
100 64 144 0x64 0144
3.14 +3e+00 3.141600E+00
10 A string
