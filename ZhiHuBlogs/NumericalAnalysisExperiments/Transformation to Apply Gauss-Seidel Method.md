---
Title: 一种处理 Gauss-Seidel 迭代法发散的方法
Author: 邱彼郑楠
Date: 2023-05-29
---

# 问题

Consider the system of linear algebraic equations: Equation (2)

$$
\begin{bmatrix}
0 & 0 & -1 & 3 & -1 & 0 \\
0 & \frac{1}{2} & 0 & -1 & 3 & -1 \\
\frac{1}{2} & 0 & 0 & 0 & -1 & 3 \\
3 & -1 & 0 & 0 & 0 & \frac{1}{2} \\
-1 & 3 & -1 & 0 & \frac{1}{2} & 0 \\
0 & -1 & 3 & -1 & 0 & 0
\end{bmatrix}\begin{bmatrix}
x_1 \\ x_2 \\ x_3 \\ x_4 \\ x_5 \\ x_6
\end{bmatrix}=\begin{bmatrix}
1 \\ \frac{3}{2} \\ \frac{5}{2} \\ \frac{5}{2} \\ \frac{3}{2} \\ 1
\end{bmatrix}
$$

(a) Implement the Gauss-Seidel method in Matlab and compute the solutions for Equation (2) for a tolerance of 1e-3.

(b) Discuss one major problem you may encounter when use Gauss-Seidel method and show how you may address. (Assume the coefficient matrix is diagonally dominant).

# Gauss-Seidel 迭代法


