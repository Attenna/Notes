# St. Petersburg Paradox — 实践作业报告 / Practical Assignment Report (中英双语) 
## 一、理论推导与期望分析 
### 1) 经典圣彼得堡游戏期望 
设第 k 次抛出为首次正面（k>=1），概率 $P(k) = (1/2)^k$，奖金为 $2^k$。 数学期望： $$ E[X] = \sum_{k=1}^{\infty} (1/2)^k \cdot 2^k = \sum_{k=1}^{\infty} 1 = +\infty $$ 因此期望发散（无穷大）。

English: Let the first head occurs on trial k (k>=1) with probability $P(k)=(1/2)^k$ and payout $2^k$. The expectation is $$ E[X] = \sum_{k=1}^{\infty} (1/2)^k \cdot 2^k = \sum_{k=1}^{\infty} 1 = +\infty $$ so the expected payoff diverges (infinite). 
### 2) 若奖金改为 $3^k$ 
$$ E[X] = \sum_{k=1}^{\infty} (1/2)^k \cdot 3^k = \sum_{k=1}^{\infty} \left(\frac{3}{2}\right)^k $$ 此为等比级数，公比 $r = 3/2 > 1$，因此级数发散，期望仍为无穷大。

English: If payout is $3^k$ instead: $$ E[X]=\sum_{k=1}^{\infty} \left(\frac{1}{2}\right)^k 3^k = \sum_{k=1}^{\infty} \left(\frac{3}{2}\right)^k $$ a geometric series with ratio $3/2>1$, so it diverges as well. 
## 二、效用函数的作用 / Role of Utility Functions 
考虑凹效用函数 $u(x)=\ln x$ 与线性效用 $u(x)=x$。 对 $u(x)=\ln x$： $$ E[u(X)] = \sum_{k=1}^{\infty} \left(\frac{1}{2}\right)^k \cdot \ln(2^k) = \sum_{k=1}^{\infty} \left(\frac{1}{2}\right)^k \cdot k \ln 2 $$ 令 $r=1/2$，已知 $$ \sum_{k=1}^{\infty} k r^k = \frac{r}{(1-r)^2} $$ 代入得 $$ \sum_{k=1}^{\infty} k \left(\frac{1}{2}\right)^k = 2 $$ 因此 $$ E[u(X)] = \ln 2 \cdot 2 = 2 \ln 2 $$ （有限）。这说明在对数效用下期望效用是有限的，因而理性决策者会基于期望效用而不是期望货币价值决定是否参与，从而解决悖论。

English: For $u(x)=\ln x$: $$ E[u(X)] = \sum_{k=1}^{\infty} \left(\frac{1}{2}\right)^k \cdot k \ln 2 $$ Using $$ \sum_{k=1}^{\infty} k r^k = \frac{r}{(1-r)^2} $$ for $r=1/2$ gives $$ \sum_{k=1}^{\infty} k \left(\frac{1}{2}\right)^k = 2 $$ Thus $$ E[u(X)] = 2 \ln 2 $$ finite. 

This shows concave utility (log) yields finite expected utility, resolving the paradox by explaining risk-averse behavior. 对线性效用 $u(x)=x$： $$ E[u(X)]=E[X]=+\infty $$ 与直觉冲突。 

English: With linear utility $u(x)=x$, $E[u(X)]$ diverges, which contradicts observed willingness-to-pay. 

对比结论：凹函数（如对数）将边际效用递减，引入风险厌恶，能解释人们不愿支付高价参与游戏。 

English: Conclusion: Concave utilities (e.g., log) decrease marginal utility and model risk aversion, explaining why people pay only a limited amount to enter the game. 

## 三、数值模拟与风险感知（代码与结果） / Simulation & Risk Perception 
代码文件：`simulate_st_petersburg.py` 运行（示例）: ```bash python3 simulate_st_petersburg.py --trials 1000 --fee 50