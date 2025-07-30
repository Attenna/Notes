## 查找单词
Finds the occurence of a giben word in a sentence and counts the number of time the wored occurs.
做 to空格 的完全匹配
copy the word in sentence to str2 after Word Division
```c
word_len = i - start_pos;
strncpy(str2,&str[start_pos],word_len);
```
Determine if String1 and String2 are the same
```c
if  (!strcmp(str1,str2));
```
得判断`str[0]` 是什么
四个判断条件
word start
skip charecters
skip spaces 
word end

有限自动机 Finite Automation Machine FAM
Automaton

state change under certain conditions

flag

开始，第一次检测到是字母
结束，第一次检测到空格到0
这样来判断单词
进行比较
count++
状态迁移回第一状态

state 变量用来记录状态，switch来控制切换，一般来说，状态的切换是通过类来实现的