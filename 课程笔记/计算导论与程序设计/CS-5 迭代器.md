### 下面能输出什么？
```c
count=0;
while (count++)
{
    printf("%d", count);
}
```
先判断count == 0，再++，所以是无输出

### 以下代码正确循环次数是多少？
```c
    int m = 10;
    int n = 100;
    int count = 0;
    while (--m)
    {
        n = 100;
        while (n--)
        {
            count++;
        }
    }
    printf("%d", count);
```
900
\--m是先减，后判断。所以是循环9次，n\--是先判断再\--，所以n循环100次（100 - 到 1，0结束循环）

## 填空题
以下代码是从键盘输入字串，从字串中将数字筛选出来，并在收到回车的时候结束判断。  
示例：  
输入：98a 7m,0  
输出：  
9  
8  
7  
0

尝试完善以下代码：

```c
#inclde <stdio.h>
int main() {
    int c = 0;
    while (scanf("%c", &c) != EOF)
    {
        if (c == '\n') {
		     break;
        }
        else if (c < '0' || c > '9') {
		    continue;
	    }
        else{
            printf("%c\n", c);
    }
}
```

### 填空题
```c
int i=10;
int sum=0;
do
{
    sum+=i;//注意循环
}while(i--);//while语句至少执行一次
printf("%d", sum);
```
以上代码的循环执行完成后  
sum 输出为 55
sum+=i; 被执行了 11 次

```c
int i=10;
int sum=0;
while(i--)//先判定了
{
    sum+=i;
}
printf("%d", sum);
```

以上代码的循环执行完成后  
sum 输出为 45
sum+=i; 被执行了 10 次

### 编程题目
从键盘获得一组大于0的数，求最小值（输入小于等于0的数字结束循环）  
例如：输入 100 90 0 三个数，循环结束，并返回 90

补全缺失的代码：

```c
int N;
int min=0;
do
{
    scanf("%d", &N);
    printf("%d",&N);
}while(N <= 0);
```
不会做

## 6-1-1 计算导论05：for循环

编写函数，根据输入的N，打印由"_"和"*"组成的倒三角。  
例如：  
输入3  
打印

```
***
_*_
```

要求：  
1、用for循环编写代码  
2、输入的N为奇数（1、3、5、7 …）

3、产生的倒三角是等边的，实心的

4、三角由 ‘*’ 组成，三角空白由 ‘_’ 填充

5、根据函数接口撰写打印代码

### 函数接口定义：

```c
int printStar ( const int N);
```

输入的N为正整数

### 裁判测试程序样例：

```c
#include <stdio.h>

int printStar ( const int N);

int main()
{
  int N;
  scanf("%d", &N);
  if(N%2) printStar (N);
  else  printf("need input uneven number!");
  return 0;
}
```

### 输入样例：

例如：

```in
5
```

### 输出样例：

在这里给出相应的输出。例如：

```out
*****
_***_
__*__
```

### 作答：
```c
#include <stdio.h>
int printStar (const int N){
    for (int i = 0; i < N / 2 + 1; i++) {//列
        for (int j = 0; j < i; j++) {//行
            printf("_");
        }
        for (int k = 0; k < N - 2 * i; k++) {
            printf("*");
        }
        for (int j = 0; j < i; j++) {
            printf("_");
        }
        printf("\n");
    }
    return 0;
}
```

