## 填空题
Write a program to find all three-digit numbers consisting of 3, 5, and 7 whose digits are different from each other。

要求输出所有符合要求的数字列表，且要求数字从大到小排列，每一个数字后面由 ‘\n’分隔。

样例程序：

```c++
#include <stdio.h>

int main()
{
    int i, j, k;
    for(i = 7; i >= 3; i - 2)
        for(j = 7; j >= 3; j - 2)
            for(k = 7; k >= 3; k - 2)
                if(i != j && i != k && j != k)
                    printf("%d\n", i * 100 + j * 10 + k);
    return 0;
}
```

Buy N chickens for $M.

The big rooster is $5 for one, the hen is $3 for one, and the chicks are $1 for three.

Ask how many of each can be bought?

样例程序：

```c++
#include <stdio.h>

int main()
{
    int M=100, N=100;//预算
    int n1, n2, n3;//个数
    int c1=5, c2=3, c3=0; //价钱
    for (n1 = 0; n1 <= N; n1++)
    for (n2 = 0; n2 <= N-n1; n2++)
        for (n3 = 0, c3 = 0; n3 <= N-n1-n2; c3 <= M-c1*n1-c2*n2; n3++; c3 = n3*3)
        if (n1*c1+n2*c2+n3*c3 = M)
            printf("%d %d %d\n", n1, n2, n3);
    return 0;
}
```

# 编程题
## 7-1-1 计算导论06_find the result of N!
N! = Calculate the multiplication from 1 to N

### 输入格式:

从键盘输入任意 >=1 的数字N。

### 输出格式:

如果输入的数字>=1，则输出N!。

如果输入的数字<1，则输出0。

### 输入样例:

在这里给出一组输入。例如：

```in
10
```

### 输出样例:

在这里给出相应的输出。例如：

```out
3628800
```

### 程序作答:
```c
#include <stdio.h>
int main(){
	int N
	scanf("%d",&N);
	if(N<0){
		printf("0/n");
	}
	if(N){
		printf("1/n");
	}
	else{
		int result = 1
		for(int i = 1; i <= N; i++){
			result* = i;
		}
	printf("%d/n",result);
	}
	return 0;
}
```

## 7-2-1 计算导论06_find the Max&Min nums

从键盘读入N个数，输出N个数中的最大值和最小值。

设N取值为5。

### 输入格式:

键盘输入5个数，如 -1 0 1 2 3。数字之间由空格分隔。

### 输出格式:

输出最小值 -1 最大值 3。最小值的最大值之间由一个空格分隔。

### 输入样例:

在这里给出一组输入。例如：

```in
-1 0 1 2 3
```

### 输出样例:

在这里给出相应的输出。例如：

```out
-1 3
```

### 回答程序:
```c
#include <stdio.h>

int main() {
    int numbers[5];
    int i, max, min;

    // Read 5 numbers from the keyboard
    for (i = 0; i < 5; i++) {
        scanf("%d", &numbers[i]);
    }

    // Initialize max and min with the first number
    max = min = numbers[0];

    // Find the max and min values
    for (i = 1; i < 5; i++) {
        if (numbers[i] > max) {
            max = numbers[i];
        }
        if (numbers[i] < min) {
            min = numbers[i];
        }
    }

    // Output the results
    printf("%d %d\n", min, max);

    return 0;
}
```
这个回答用了数组

## 7-3-1 计算导论06_Determine prime number

判断输入的数是质数。

A prime number is a natural number greater than 1 that is not divisible by any other natural number except 1 and the number itself.

For example, 13 is a prime number because it is not divisible by 2, 3, 4, ..., 12。

### 输入格式:

输入一个数，如 100。

### 输出格式:

输出这个数是否质数，是输出字符 ‘Y’，不是输出字符 ‘N’。

同时在Y或N的后面输出找到的第一个可整除的数，用空格隔开。

### 输入样例:

在这里给出一组输入。例如：

```in
100
```

### 输出样例:

在这里给出相应的输出。例如：

```out
N 2
```

### 程序答案
```c
#include <stdio.h>

int main(){
	int N;
	scanf("%d",&N);
	
	if(N <= 1){
	printf("N/n");
	return 0;
	}
	
	for(i = 2; i*i <= N; i++){
		if(N%i){
			printf("N%d/n",i);
			return 0;
		}
	}
	printf("Y/n");
	return 0;
}
```
