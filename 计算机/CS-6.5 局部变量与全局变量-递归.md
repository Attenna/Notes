Scope ia the sction of the program where the variable is valid or "known"
A variable with a local scope has had sorage set aside for it by a declaration statement made within a fincrion body 
a variable with global scope is one whose storage has been created for it by a declaration statement located ourside any function
If variables created inside a function are avaliable only to the function itself(local scope), they are said to be local to the function, of local variables.
if variable was created outside all the functions 
\
```c
//variable scope
int x; //这会独立地写在内存的global区
void compare(int y)
{
	int x = 10;
	if(x>y)
	{
		printf("%d>%d\n",x,y);
	}
	else
	{
		printf(")
	}
}
```
优先找本地定义的

递归调用复杂度太高了，解决问题方法

算法实现

构建单映
	1，全局变量
	2，static 返回static的值，做成指针

static 
	声明 函数内使用 静态  调用函数的时候被创建，函数结束不释放，再次使用时直接调用
		static *int* *XXX*
		但依然是函数内的变量
		静态表示的是 调用-释放 的静态，访问权限还是在function里面，main访问不了
extern
	兼容用
auto

register（被抛弃）

什么是<stdio.h>
\*.h头文件
接口定义文件

库
	lib静态 dll动态 (windows)
	so (linux)

例子：写一个进制转换函数
num = num%2^n-1
	=V_n-2\*2^n-2……
	计算余项
	loop until n == 0
	print each digit
	打印10进制，按照10除