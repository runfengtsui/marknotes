---
Title: 带权函数的 Newton-Cotes 数值积分公式
Author: 邱彼郑楠
Date: 2023-05-17
---

# 一道数值积分题目

> In this question, we consider different numerical quadratures for approximating the following two integrals
> $$
I_c=\int_0^1 \frac{\cos x}{\sqrt{x}}\,\mathrm{d}x
\quad\text{and}\quad
I_s=\int_0^1 \frac{\sin x}{\sqrt{x}}\,\mathrm{d}x
> $$
> (1-a) Use the composite trapezoidal rule with n intervals of equal length $h=\dfrac{1}{n}$ (n can be hundreds to 1000), "ignoring" the singularity at $x=0$ (i.e., arbitrarily using zero as the value of the integrand at $x=0$). Display your observations from the numerical results.
>
> (1-b) Use the composite trapezoidal rule over the interval $[h,1]$ with $n-1$ intervals of length $h=\dfrac{1}{n}$ in combination with a weighted Newton-Cotes rule with weight function $w(x)=x^{-\frac{1}{2}}$ over the interval $[0,h]$. Give a few remarks on the performance by comparing the numerical results obtained in (1-a).
>
> (1-c) Make the change of variables $x=t^2$ and apply the composite trapezoidal rule to the resulting integrals. Make more comparisons on the performance the numerical methods used.
>
> (1-d) You may now consider more advanced methods (e.g., composite Simpson, Gauss-Legendre quadrature etc) on the integrals obtained in (1-c) and show your observations and comparisons.

上面这道题目来自于某大学数值分析的上机实验, 以含瑕点 $x=0$ 的积分 $I_c$ 和 $I_s$ 来讨论各种数值积分方法的表现. 这个题目分别需要实现复合梯形公式, 复合 Simpson 公式以及 Gauss-Lengendre 公式, 整体的难度并不大.

但是这道题的 (1-b) 提出了一个 **a weighted Newton-Cotes rule with weight function** 的思路. 带权函数的数值积分公式不是没有, 不过目前各种教材上都是 Gauss
