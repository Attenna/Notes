### Automation
#### Finite Automata Machine(FAM)
#### Finite State Machine(FSM)

老师不喜欢焊电路板，只喜欢敲代码。他本科是电子信息工程的。老师喜欢捞人。喜欢顺便谈论一下时事。

马尔可夫链也是状态迁移
状态机是离散的

形式化定义：
DFA是一个五元组 $M = (Q,T,\sigma, q_0,F)$
其中： df54 
$Q$: 有限的状态集合
$T$: 有限的输入字母表
 $\sigma$ : 转换函数，是$Q\times T$到$Q$的映射
$q_0$:: 初始状态，$q_0 \in Q$
$F$ : 终止状态

描述一个有限自动机的工作状况，可以使用STD来描述（状态转换图）

### Word Segmentation
Finds the occurrence of a given word in a sentence and counts the number of times the word occurs
`To be or not to be is a question\0`注意，结尾是`\0`
首字母，尾字母最后面还得是空格或`\0`

