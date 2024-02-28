---
Title: Nonlinear Numerical Analysis
Author: 邱彼郑楠
Date: 2024-02-27
Modified: 2024-02-28
---

# 开映像, 闭映像, 连续映像

1. $\mathbb{R}^n$ 中的子集 $D$ 的 **相对开集** 不一定是 $\mathbb{R}^n$ 的 **开集**, 它只是 $\mathbb{R}^n$ 中的某个开集与 $D$ 的交集. 若 $D$ 为 $\mathbb{R}^n$ 的开集, 两个开集的交集自然还是开集, 也就是 $D$ 的相对开集为 $\mathrm{R}^n$ 的开集. **相对闭集** 与 **闭集** 也是类似的.
2. 开映像, 闭映像, 连续映像互不蕴含.

# 向量值函数的连续性与可微性

1. **半连续性** 是说方向连续性, 即固定某一方向后是连续的; **连续性** 和方向无关了, 增量可以是任意方向的. 即 **连续蕴含着半连续**.

2. 相应的, **Gateaux 可微** 也是和方向相关的. Gateaux 可微不蕴含连续性, 只能蕴含 **半连续性**.

3. 利用分量的方法可以求出 Gateaux 导数 $\boldsymbol{F}^\prime \left(\boldsymbol{x}\right)$ 为 $\boldsymbol{F}\left(\boldsymbol{x}\right)$ 在点 $\boldsymbol{x}$ 处的 Jacobi 矩阵.
但是, Jacobi 矩阵存在, 即所有偏导数存在, 不能蕴含 Gateaux 可微. 如映像 $f: \mathbb{R}^2\to\mathbb{R}$ 定义为
$$
f(x_1,x_2)=\begin{cases}
x_1, & \text{if}\; x_2=0;\\
x_2, & \text{if}\; x_1=0; \\
1,   & \text{else},
\end{cases}
$$
偏导数
$$
\frac{\partial f(\boldsymbol{0})}{\partial x_1}=\lim_{x_1\to 0} \frac{f(x_1,0)-f(0,0)}{x_1-0}=1,
\frac{\partial f(\boldsymbol{0})}{\partial x_2}=\lim_{x_2\to 0} \frac{f(0,x_2)-f(0,0)}{x_2-0}=1,
$$
都存在. 但是取 $\boldsymbol{h}=(h_1,h_2)^\mathrm{T}\in\mathbb{R}^2$, 其中 $h_1,h_2\neq 0$, 则 $f(\boldsymbol{h})=1$. 从而
$$
f(t\boldsymbol{h})-f(\boldsymbol{0})-tA \boldsymbol{h}=1-tA \boldsymbol{h},
$$
显然
$$
\lim_{t\to 0} \frac{1}{t}\left\lVert f(t \boldsymbol{h})-f(\boldsymbol{0})-tA \boldsymbol{h}\right\rVert=\lim_{t\to 0} \frac{1}{t}\left\lVert 1-tA \boldsymbol{h}\right\rVert\neq 0.
$$
即 $f(\boldsymbol{x})$ 在 $\boldsymbol{0}$ 处不 Gateaux 可微.

4. **Frechet 可微** 对应的与方向无关, 可以推出连续性, 连续性是 Frechet 可导的 **必要条件**. 自然 **Frechet 可微蕴含 Gateaux 可微, 且 Frechet 导数与 Gateaux 导数相等**. 但是 Gateaux 可微不蕴含 Frechet 可微.

5. 处处存在偏导数但不 Frechet 可导的例子, 映像 $F:\mathbb{R}^2\to\mathbb{R}$ 为
$$
F(\boldsymbol{x})=F(x_1,x_2)=\begin{cases}
\dfrac{x_1^2x_2}{x_1^4+x_2^2}, & \text{if}\; \boldsymbol{x}\neq \boldsymbol{0} \\
0                             & \text{if}\; \boldsymbol{x}=\boldsymbol{0}.
\end{cases}
$$
易得
$$
\frac{\partial F(\boldsymbol{0})}{\partial x_1}=\lim_{x_1\to 0} \frac{F(x_1,0)-F(0,0)}{x_1-0}=0,
\frac{\partial F(\boldsymbol{0})}{\partial x_2}=\lim_{x_2\to 0} \frac{F(0, x_2)-F(0,0)}{x_2-0}=0,
$$
即 $F(\boldsymbol{x})$ 在 $\mathbb{R}^2$ 上处处存在偏导数, 但是 $F(\boldsymbol{x})$ 在 $\boldsymbol{0}$ 处不连续, 自然不 Frechet 可导.

