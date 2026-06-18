#### 题目描述

输入一个正整数n, 请按照字典序输出1-n的全排列。

#### 输入

输入包含多组测试用例。  
每组数据占一行，包含一个正整数n(n<10)。

#### 输出

每个排列输出一行，每个数字后面跟一个空格。  
具体格式参加样例的输出。

#### 样例输入 Copy

3
2

#### 样例输出 Copy

1 2 3 
1 3 2 
2 1 3 
2 3 1 
3 1 2 
3 2 1 
1 2 
2 1
怎么求全排列？
如何让它不重复不漏？
用一个数组path保存当前构造排列
用一个布尔数组used标记数字1~n是否已经在当前排列使用过。
递归函数设计：
函数参数为当前要填充的位置pos
当pos == n时，填满了所有位置，就输出path
否则尝试每个数字i，如果used\[i]是false，那么i就没用过，那么就把它放进去，used\[i]标记为true。然后递归下一个。此时，下一层就可以自动处理未来的事情了。因此在本层回溯，重新把used\[i]标记为false。
## 二、标准模板（C++）
```cpp
#include <iostream>
#include <cstring>
using namespace std;

const int MAXN = 10;
int path[MAXN];   // 保存当前排列
bool used[MAXN];  // 标记数字是否用过
int n;

// 递归：填第 pos 个位置
void dfs(int pos)
{
    // 递归出口：已经填满 n 个数
    if(pos == n)
    {
        // 输出
        for(int i=0; i<n; i++)
            cout << path[i] << " ";
        cout << endl;
        return;
    }

    // 从小到大尝试每个数字（保证字典序）
    for(int i=1; i<=n; i++)
    {
        if(!used[i])  // 没用过
        {
            used[i] = true;   // 标记使用
            path[pos] = i;    // 放入当前位置
            dfs(pos + 1);     // 递归填下一个位置
            used[i] = false;  // 回溯！恢复现场
        }
    }
}

int main()
{
    // 多组输入
    while(cin >> n)
    {
        memset(used, 0, sizeof(used)); // 清空标记
        dfs(0);  // 从第 0 个位置开始填
    }
    return 0;
}
```