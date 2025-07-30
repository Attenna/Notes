```c
#include <stdio.h>

int main(void){
	int i = 100;
	{
		int i = 110;
		printf("%d",i);
	}
	printf("%d",i);
	return 0;
}
```
函数的作用域，也是在文件开始，文件结束的。

```c
#include <stdio.h>

void func(void);

int main(void)
{
	extern int count;//别急，有反转
	func();
	count++;
	printf("In main, count = %d\n",count);
	return 0;
}

int count;

void func(void){
count++;
printf("In func, count = %s\n",count);
}
```

## 原型作用域（pronotype scope)

原型作用域只适用于在函数原型中声明的参数名。甚至你实际使用的变量名字和形式参数也可以不一样。

## 函数作用域（function scope）

函数作用域只适用于goto语句的标签。

## 定义和声明

当一个变量被定义的时候，编译器为变量申请内存，并填充一些值

当一个变量被声明的时候，编译器知道变量定义在了其它地方。

声明通知编译器该变量名及相关的类型已经存在了，不用再定义一次

## 链接属性

先编译，再链接。
编译把c语言写成机器码，链接让头文件和目标文件合并，得到可执行程序。

### external
多个文件中声明同名标识符表示同一个实体
### internal
单个文件
### none
各个独立。

只有具备文件作用域的标识符才能拥有external 或 internal 的链接属性。
默认情况下，具备文件作用域的标识符拥有external属性。无论在文件中声明多少次，都视为同一个东西。

