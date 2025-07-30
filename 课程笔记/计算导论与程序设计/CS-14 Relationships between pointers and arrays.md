```c
int a[5]
int *b = a
*(a+1)
```
但是数组和指针是完全不同的两个东西
`sizeof`函数一个数组
把指针当成一个一维数组来管理。
```c
p[1] = *(p+1)
```
```c
int len = actual required size;
int val[len];
int * pval;
pval = malloc(sizeof(int)*len);
```
## memory malloc
```c
vaoid *malloc(size t size);//无类型指针
```
```c
(int*)p
```
## pointers and multi-dimensional arrays
### Advanced pointer Notation 指针指向数组内容
```c
int **p1 = nums
```
指针是变量，二重指针是指向一个变量的地址，光定义二重指针是没法反映数组的列的
二维数组通过列的数量（行的长度）来进行数组的遍历。
### Convert 2D to 1D Array
### Pointer variable to two dimension
```c
int val[ROWS][COLUMNS] = {{1,2,3,4},{11,12,13,14},{21,22,23,24}};
int (*pt1)[COLUMNS];
pt1 = val;
int* pt2
```
指针数组是真正地指向了每一行，真的有一个数组，指针数组的每一个单元又指向了原数组的每一行。
二维数组可以当作参数给函数

## Example5: get Multi-Inputs
传地址，使函数调用到合适的变量。
堆内存，栈内存
堆和栈是没关系的

## Example: Protocol Stack
回调栈

### Homework: Hanoi
Implementing Hnnukah'h Tower using Recurion
```c
void Hanoi(int n, char from, char temp, char to, int *move, void(*moveN)(init))
```
How to realize hanoi.
### 数组遍历，报数游戏

\--------------------------------------------------------------------------------

### 数组与指针的关系

```c
int a[5];
int *b = a;
*(a + 1);
```

- **数组和指针的关系**：数组名 `a` 是一个指向数组第一个元素的指针。`int *b = a;` 将指针 `b` 指向数组 `a` 的第一个元素。
- **指针运算**：`*(a + 1)` 表示数组 `a` 的第二个元素。

### `sizeof` 函数

- **数组**：`sizeof(a)` 返回数组 `a` 所占的总字节数。
- **指针**：`sizeof(b)` 返回指针 `b` 所占的字节数（通常是4或8字节，取决于系统）。

### 指针与一维数组

```c
p[1] = *(p + 1);
```

- **等价表达式**：`p[1]` 等价于 `*(p + 1)`，表示指针 `p` 指向的数组的第二个元素。

### 动态内存分配

```c
int len = actual_required_size;
int val[len];
int *pval;
pval = malloc(sizeof(int) * len);
```

- **动态数组**：`int val[len];` 定义一个长度为 `len` 的数组（C99标准）。
- **动态内存分配**：`pval = malloc(sizeof(int) * len);` 分配 `len` 个 `int` 类型大小的内存空间，并将指针 `pval` 指向这块内存。

### `malloc` 函数

```c
void *malloc(size_t size); // 无类型指针
```

- **无类型指针**：`malloc` 返回一个 `void*` 类型的指针，需要强制转换为具体类型。

```c
(int*)p;
```

- **强制类型转换**：将 `void*` 类型的指针 `p` 转换为 `int*` 类型。

### 指针与多维数组

#### 高级指针表示法

```c
int **p1 = nums;
```

- **二级指针**：`int **p1` 是一个指向指针的指针，通常用于指向二维数组。
- **指针与数组的关系**：定义一个二级指针并不能完全反映数组的列信息，需要进一步处理。

### 示例代码

以下是一些示例代码，帮助理解指针与数组的关系：

#### 一维数组与指针

```c
#include <stdio.h>

int main() {
    int a[5] = {1, 2, 3, 4, 5};
    int *b = a;
    printf("a[1] = %d\n", a[1]);
    printf("*(a + 1) = %d\n", *(a + 1));
    printf("b[1] = %d\n", b[1]);
    printf("*(b + 1) = %d\n", *(b + 1));
    return 0;
}
```

#### 动态内存分配

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int len = 5;
    int *pval = (int*)malloc(sizeof(int) * len);
    for (int i = 0; i < len; i++) {
        pval[i] = i + 1;
        printf("pval[%d] = %d\n", i, pval[i]);
    }
    free(pval); // 释放内存
    return 0;
}
```

#### 二维数组与指针

```c
#include <stdio.h>

int main() {
    int nums[2][3] = {{1, 2, 3}, {4, 5, 6}};
    int (*p)[3] = nums;
    printf("nums[1][2] = %d\n", nums[1][2]);
    printf("*(*(p + 1) + 2) = %d\n", *(*(p + 1) + 2));
    return 0;
}
```

希望这些补充对你有帮助！如果有任何问题，随时问我哦。