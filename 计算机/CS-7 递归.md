function calls 函数调用
	本地变量为什么别人不能用？![[Pasted image 20241107180945.png]]
	返回到调用点，继续执行后面的语句，调用，执行，再返回到调用点
栈
=
stack
先入后出

变量 就是 地址 名字
0x1234

优先访问本地变量

指针：top 栈顶
弹栈
运行环境
=
每一行都有地址
操作数

Recursive Algorithm
=
求阶乘
```
const int N = 10;
int facctorial;

int F(int n){
	if(n>1)
		return n * F(n-1);
	else
		return 1;
}

fatorial = F(N)
```
状态机也是一种递归
递归有两种
indirect 
mutal recursion
递归调用过程，回归返回过程 
计算数字长度：
length(num) = 1 if num<10
length(num) = length((num/10))+1 if num > 10
```
int len = 1;
while ((num = num/10)>0){
	len++;
}
return len;
```
赋值有最低优先级，所以要加括号
汉诺塔


## 函数调用方法
值传递和指针传递