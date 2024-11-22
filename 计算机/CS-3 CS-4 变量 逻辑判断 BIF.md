以下打印结果是什么？
```c
int x=10;
int y=9;
printf("%d", x > y);
```
1
因为是逻辑判断，True与1等价

希望判断x是否为0，如果不为0则打印TRUE，以下哪一种条件表达式撰写是正确的？
	```
```c
int x = 0;
if( ________ ) printf("TRUE");
else printf("FALSE");
```
x != 0

以下表达式正确的是(编译器支持C99以上版本)：
	```
```c
	A.
	int a, b, c;  
	a = b = c = 10;
	
	B.
	int a = 10, b = 10, c = 10;
	
	C.
	int a = 10;  
	int b = a;  
	int c = b;
	
	D.
	int a, b, c;  
	a = 10;  
	b = a;  
	c = b;
```
???
以下程序运行结果正确的是
```c
int main(){
	int x = 10;
	int y = 5;
	if(y=x){
		printf("%d",x);
	}else{
		printf("%d",y);
	}
	printf("%d",y);
	return 0;
}
```
因为赋值了，答案是1010

有下列swich语句
```c
switch (k)
{
    case 1:printf(“A”);
    case 2:printf(“B”);break;
    case 3:
    case 4:printf(“C”);
    case 5:printf(“D”);break;
    default :printf(“Error”);
}

```
当```k = 2,3,4,6```时，输出结果分别是
B CD CD Error

从键盘上输入一个数字星期（用整型变量x表示），然后输出它对应的的英文，如果输入的数据不在1到7的范围，请输出"-1"（不包含引号）。  
其对应关系是： 1 Monday 2 Tuesday 3 Wednesday 4 Wednesday 5 Friday 6 Saturday 7 Sunday
```c
#include <stdio.h>
int main(void)
{int k;  //变量定义
 scanf("%d",&k);  //数据输入
  swich(k)//开始判断
 {case 1:printf("Monday\n");break;
  case 2:printf("Tuesday\n");break;
  case 3:printf("Wednesday\n");break;
  case 4:printf("Wednesday\n");break;
  case 5:printf("Friday\n");break;
  case 6:printf("Saturday\n");break;
  case 7:printf("Sunday\n");break;
  default:printf("-1\n");break;
 }
 return 0;
}
```
