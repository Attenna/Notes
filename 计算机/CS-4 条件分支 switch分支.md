## 凯撒密码
密码学中，凯撒密码（Caesar Cipher）是一种最简单的加密技术，其核心思想是替换加密。即将输入的字母根据字母表上的顺序，向前或向后偏移固定的数目，形成密文。如：向后偏移2位，则 A 变成 C（相当于 'A'+2）。  
在应用中，可以将字母表中的 A-Z a-z 0-9 扩展为大循环，形成 A B ~ Z a b ~ z 0 1 ~ 9 A B ~ Z...为基础的链，用以进行映射。如：输入Z，向后偏移2位，则Z变成b。输入9，向后偏移2位，则9变成B。

本题要求：将以下代码补充完整，用于将输入的字符转换为凯撒加密的密文。
### 代码段：

```c
char CaesarCipher ( const char IN, const int D )
{
    int CC=IN;
        
        ....
    return CC;    
}
```

其中  
变量 `IN` 是输入的字符（取值为：A~Z，a~z，0~9，还包括标点符号和空格）（注意：标点符号和空格不转换）  
变量 `D` 是偏移（取值为 -10=<D<=10
### 裁判测试程序样例：

```c
#include <stdio.h>

char CaesarCipher ( const char IN, const int D );

int main()
{

  int IN='A';
    int D=2;

  printf("%c", CaesarCipher(IN, D));

  return 0;

}
```

### 输入样例：

输入。例如：

```in
A 2
```

### 输出样例：

```out
C
```

### 提交程序：
```c
#include <stdio.h>
char CaesarCipher (const char IN, Const int D){
	int CC = IN;
	int i;
	if(D>=0){
		for(i = 1; i <= D; i++){
			switch(CC){//拼接成环
			case('9'):CC = 'A';break;
			case('Z'):CC = 'a';break;
			case('z'):CC = '0';break;
			default:CC++;break;//在分段内直接默认加1，ACSCII是和整数等价的
			}
		}
	}
	else{
		for(i = 1; i<= -D; i++){
			switch(CC){
			case('A'):CC = '9';break;
			case('a'):CC = 'Z';break;
			case('0'):CC = 'z';break;
			defaul:CC--; break;//考虑负偏移情况
			}
		}
	}
	return CC;
}
```

## 6-1-2 计算导论04：分支-Switch

题目要求：  
1、输入每月sales，数据类型为整数  
2、使用参考书 Program 4.5 提供的判断条件  
3、使用 switch 实现 income 计算逻辑，并输出

![C.png](https://images.ptausercontent.com/3753e7e6-2e98-4423-b1d7-f2e1a0f71bdd.png)

例如：输入10000， 输出计算方法：450+10000*0.05  
注意：sales取值可以超过100000

### 接口代码：

```c++
float income ( const int IN )
{
    float OUT=0;
    ......
    return OUT;
}
```

其中，  
ID是输入的sales数量  
OUT是计算的income取值

### 裁判测试程序样例：

```c++

#include <stdio.h>

float income ( const int IN );

int main()
{
  int IN;
  scanf("%d", &IN);
  if(IN>=1000) printf("%.2f", income(IN));
  return 0;
}
```

### 作答程序：
```c
#include <stdio.h>
float inclome (const int IN){
	float OUT = 0;
	
    switch (IN / 10000) {//通过地板除法筛选数位，数量级
        case 0:
            OUT = 400 + IN * 0.03;
            break;
        case 1:
            OUT = 450 + IN * 0.05;
            break;
        case 2:
            OUT = 500 + IN * 0.09;
            break;
        case 3:
            OUT = 525 + IN * 0.12;
            break;
        case 4:
            OUT = 550 + IN * 0.14;
            break;
        case 5:
            OUT = 575 + IN * 0.16;
            break;
        default:
            OUT = 575 + IN * 0.16;
            break;
    }

    return OUT;
}
```
