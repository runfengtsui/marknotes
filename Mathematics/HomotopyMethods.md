---
Title: 同伦方法
Author: 邱彼郑楠
Date: 2024-03-30
Modified: 2024-03-30
---

# 预备知识

1. $\R^m$ 中的任意紧集上的连续映射都可由光滑映射任意逼近.

> **Theorem**. 设 $X\sub\R^m$ 是紧集, $f: X\to\R^n$ 是连续映射, 则对任意 $\varepsilon > 0$, 存在光滑映射 $g: X\to\R^n$, 使得对任意 $x\in X$, 成立
> $$ \left\lVert f(x)-g(x)\right\rVert < \varepsilon. $$

## 正则值

> **Definition**. 设 $f:D\sub\R^m\to\R^n$ 是光滑映射, 对 $D$ 中的某一点 $\boldsymbol{x}_0$, 如果 $f$ 在 $\boldsymbol{x}_0$ 处的 Jacobi 矩阵 $\dfrac{\partial f}{\partial x}\left(\boldsymbol{x}_0\right)$ 行满秩, 则称 $\boldsymbol{x}_0$ 是映射 $f$ 的正则点. 若 $\boldsymbol{x}_0$ 不是映射 $f$ 的正则点, 即映射 $f$ 在 $\boldsymbol{x}_0$ 点处的 Jacobi 矩阵行降秩, 则称 $\boldsymbol{x}_0$ 是映射 $f$
