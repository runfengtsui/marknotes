---
Title: Cauchy-Binet公式及其应用
Author: 邱彼郑楠
Date: 2021-05-08
Modified: 2021-05-12 21:10
Category: 高等代数
Tags: Cauchy-Binet 公式
Slug: application-cauchy-binet

---

## Binet-Cauchy 公式

我们知道，方阵的行列式不是方阵的线性函数，即对 $\forall \lambda\in F,A,B\in F^{n\times n}$，有 $det(A+B)\neq detA+detB$ 和 $det(\lambda A)\neq \lambda detA$；而方阵的行列式是方阵的可乘函数，即 $det(AB)=detA\cdot detB$. 那么如果 $A,B$ 不是方阵，而是长方矩阵，那么就可以推广得到 **Cauchy-Binet** 公式。

**Theorem(Cauchy-Binet)**$^{[1]}$ 设 $A=(a_{ij})$ 是 $m\times n$ 矩阵，$B=(b_{ij})$ 是 $n\times m$ 矩阵，$A\begin{pmatrix}i_1 & \cdots & i_s \\ j_1 & \cdots & j_s\end{pmatrix}$ 表示 $A$ 的一个 $s$ 阶子式，它由 $A$ 的第 $i_1,\cdots,i_s$ 行与第 $j_1,\cdots,j_s$ 列交点上的元素按原次序排列组成的行列式。同理定义 $B$ 的 $s$ 阶子式，则 

(1) 若 $m>n$，必有 $|AB|=0$;

(2) 若 $m\le n$，必有
$$
|AB|=\displaystyle\sum_{1\le j_1<j_2<\cdots<j_m\le n}A\begin{pmatrix} 1 & 2 & \cdots & m \\ j_1 & j_2 & \cdots & j_m \end{pmatrix}B\begin{pmatrix} j_1 & j_2 & \cdots & j_m \\ 1 & 2 & \cdots & m \end{pmatrix}.
$$

**Proof**. 令 $C=\begin{pmatrix} A & 0  \\ -I_n & B \end{pmatrix}$. 我们将用不同的方法来计算行列式 $|C|$.

首先，对 $C$ 进行第三类分块初等变换得到矩阵 $M=\begin{pmatrix} 0 & AB \\ -I_n & B \end{pmatrix}$. 事实上，$M$ 可写为
$$
M=\begin{pmatrix}
I_m & A \\
0 & I_n
\end{pmatrix}C,
$$
因此 $|M|=|C|$. 用 Laplace 定理来计算 $|M|$，按前 $m$ 行展开得
$$
|M|=(-1)^{(n+1+n+2+\cdots+n+m)+(1+2+\cdots+m)}|-I_n||AB|=(-1)^{n(m+1)}|AB|.
$$
再来计算 $|C|$，用 Laplace 定理按前 $m$ 行展开。这时若 $m>n$，则前 $m$ 行中任意一个 $m$ 阶子式都含有至少一列全为零，因此行列式值等于零，即 $|AB|=0$. 若 $m\le n$，由 Laplace 定理得
$$
|C|=\displaystyle\sum_{1\le j_1<j_2<\cdots<j_m\le n}A\begin{pmatrix} 1 & 2 & \cdots & m \\ j_1 & j_2 & \cdots & j_m \end{pmatrix}C \begin{pmatrix} 1 & 2 & \cdots & m \\ j_1 & j_2 & \cdots & j_m \end{pmatrix},
$$
其中 $C\begin{pmatrix}1 & 2 & \cdots & m \\ j_1 & j_2 & \cdots & j_m \end{pmatrix}$ 是 $A\begin{pmatrix} 1 & 2 & \cdots & m \\ j_1 & j_2 & \cdots & j_m \end{pmatrix}$ 在矩阵 $C$ 中的代数余子式。显然
$$
C\begin{pmatrix}
1 & 2 & \cdots & m \\
j_1 & j_2 & \cdots & j_m
\end{pmatrix}=(-1)^{\frac{1}{2}m(m+1)+(j_1+j_2+\cdots+j_m)}|-e_{i_1},-e_{i_2},\cdots,-e_{i_{n-m}},B|,
$$
其中 $i_1,i_2,\cdots,i_{n-m}$ 是 $C$ 中前 $n$ 列去掉 $j_1,j_2,\cdots,j_m$ 列后余下的列序数，$e_{i_1},e_{i_2},\cdots,e_{i_{n-m}}$ 是相应的 $n$ 维标准单位列向量。记
$$
|N|=|-e_{i_1},-e_{i_2},\cdots,-e_{i_{n-m}}|,
$$
现来计算 $|N|$. $|N|$ 用 Laplace 定理按前 $n-m$ 列展开。注意只有一个子式非零，其值等于 $|-I_{n-m}|=(-1)^{n-m}$. 而这个子式的余子式为
$$
B\begin{pmatrix}
j_1 & j_2 & \cdots & j_m \\
1 & 2 & \cdots & m
\end{pmatrix}.
$$
因此
$$
|N|=(-1)^{(n-m)+(i_1+i_2+\cdots+i_{n-m})+(1+2+\cdots+n-m)}B\begin{pmatrix}
j_1 & j_2 & \cdots & j_m \\
1 & 2 & \cdots & m
\end{pmatrix}.
$$
注意到 $(i_1+i_2+\cdots+i_{n-m})+(j_1+j_2+\cdots+j_m)=1+2+\cdots+n$, 综合上面的结论，通过简单计算不难得到
$$
|AB|=\displaystyle\sum_{1\le j_1<j_2<\cdots<j_m\le n}A\begin{pmatrix} 1 & 2 & \cdots & m \\ j_1 & j_2 & \cdots & j_m \end{pmatrix}B\begin{pmatrix} j_1 & j_2 & \cdots & j_m \\ 1 & 2 & \cdots & m \end{pmatrix}.
$$

## Binet-Cauchy 公式在恒等式中的应用

**Binet-Cauchy** 公式有很多方面的应用，比如证明 Lagrange 恒等式，Cauchy- Schwarz 不等式，计算一些特殊的 $n$ 阶行列式。下面我们先来看其在恒等式证明中的应用。

**Question 1**.$^{[1]}$ 证明 Lagrange 恒等式($n\ge2$):
$$
\displaystyle\left(\sum_{i=1}^n a_i^2\right)\left(\sum_{i=1}^n b_i^2\right)-\left(\sum_{i=1}^n a_ib_i\right)^2=\sum_{1\le i<j\le n}(a_ib_j-a_jb_i)^2.
$$

**Proof**. 左边的表达式写成行列式的形式如下
$$
\begin{vmatrix}
\displaystyle\sum_{i=1}^n a_i^2 & \displaystyle\sum_{i=1}^n a_ib_i \\
\displaystyle\sum_{i=1}^n a_ib_i & \displaystyle\sum_{i=1}^n b_i^2
\end{vmatrix}.
$$
这个行列式对应的矩阵可化为
$$
\begin{pmatrix}
a_1 & a_2 & \cdots & a_n \\
b_1 & b_2 & \cdots & b_n 
\end{pmatrix}\begin{pmatrix}
a_1 & b_1 \\
a_2 & b_2 \\
\vdots & \vdots \\
a_n & b_n
\end{pmatrix}.
$$
用 Cauchy-Binet 公式得
$$
\displaystyle\begin{vmatrix} \displaystyle\sum_{i=1}^n a_i^2 & \displaystyle\sum_{i=1}^n a_ib_i \\ \displaystyle\sum_{i=1}^n a_ib_i & \displaystyle\sum_{i=1}^n b_i^2 \end{vmatrix}=\sum_{1\le i<j\le n}\begin{pmatrix} a_i & a_j \\ b_i & b_j \end{pmatrix}\begin{pmatrix} a_i & b_i \\ a_j & b_j \end{pmatrix}=\sum_{1\le i<j\le n}(a_ib_j-a_jb_i)^2.
$$

注意到，上述证明过程中行列式的值是非负的，这样我们就得到了Cauchy- Schwarz不等式。另外，类似于上面的证明过程，我们可以使用 Cauchy-Binet 公式证明比 Lagrange 恒等式更一般的结论 Cauchy 恒等式$^{[2]}$ 。当然，也可以使用其他方法证明这恒等式，但是显然没有使用 Cauchy-Binet 公式证明来得简洁。

## Binet-Cauchy 公式在行列式计算中的应用

Binet- Cauchy 公式在行列式中应用最多的情形是 $m=n$ 时方阵乘积的行列式等于方阵行列式的乘积。而对于一些特殊的行列式，我们可以把这个行列式对应的矩阵写成两个长方阵的乘积，然后利用 Binet-Cauchy 公式进行分类讨论，可以参考下面两道例题:

**Question 2**.$^{[3]}$ 计算行列式:
$$
\begin{vmatrix}
x_1y_1+1 & x_1y_2+1 & \cdots & x_1y_n+1 \\
x_2y_1+1 & x_2y_2+1 & \cdots & x_2y_n+1 \\
\vdots & \vdots & \ddots & \vdots \\
x_ny_1+1 & x_ny_2+1 & \cdots & x_ny_n+1
\end{vmatrix}.
$$

**Solution**. 记此行列式为 $|A|$，则有
$$
|A|=\begin{vmatrix}\begin{pmatrix}
x_1 & 1 \\
x_2 & 1 \\
\vdots & \vdots \\
x_n & 1 
\end{pmatrix}\begin{pmatrix}
y_1 & y_2 & \cdots & y_n \\
1 & 1 & \cdots & 1
\end{pmatrix}\end{vmatrix}.
$$
由 Binet-Cauchy 公式，当 $n>2$ 时，$|A|=0$; 当 $n=2$ 时，
$$
|A|=\begin{vmatrix}\begin{pmatrix}
x_1 & 1 \\
x_2 & 1
\end{pmatrix}\begin{pmatrix}
y_1 & y_2 \\
1 & 1
\end{pmatrix}\end{vmatrix}=\begin{vmatrix}
x_1 & 1 \\
x_2 & 1 
\end{vmatrix}\begin{vmatrix}
y_1 & y_2 \\ 
1 & 1
\end{vmatrix}=(x_1-x_2)(y_1-y_2).
$$
当 $n=1$ 时，$|A|=x_1y_1+1$.

**Question 3**.$^{[3]}$ 计算行列式:
$$
\begin{vmatrix}
x_1-y_1 & x_1-y_2 & \cdots & x_1-y_n \\
x_2-y_1 & x_2-y_2 & \cdots & x_2-y_n \\
\vdots & \vdots & \ddots & \vdots \\
x_n-y_1 & x_n-y_2 & \cdots & x_n-y_n
\end{vmatrix}.
$$

**Solution**. 记此行列式为 $|B|$，则有
$$
|B|=\begin{vmatrix}\begin{pmatrix}
x_1 & -1 \\
x_2 & -1 \\
\vdots & \vdots \\
x_n & -1
\end{pmatrix}\begin{pmatrix}
1 & 1 & \cdots & 1 \\
y_1 & y_2 & \cdots & y_n
\end{pmatrix}\end{vmatrix}.
$$
由 Binet-Cauchy 公式，当 $n>2$ 时，上式右端乘积的行列式为零;当 $n=2$ 时,
$$
|B|=\begin{vmatrix}\begin{pmatrix}
x_1 & -1 \\
x_2 & -1
\end{pmatrix}\begin{pmatrix}
1 & 1 \\
y_1 & y_2
\end{pmatrix}\end{vmatrix}=\begin{vmatrix}
x_1 & -1 \\
x_2 & -1 
\end{vmatrix}\begin{vmatrix}
1 & 1 \\
y_1 & y_2
\end{vmatrix}=(x_1-x_2)(y_1-y_2).
$$
当 $n=1$ 时，$|B|=x_1-x_2$.

可见，Binet-Cauchy 公式是处理这种值随阶数变化而变化的行列式的有力工具。Binet-Cauchy 公式应用最多的还是 $m=n$ 的情形，具体可以参考文献[4]第三章第二节习题第4题的前三小题，这里不再赘述。下面给出轮回方阵的行列式的应用 Cauchy- Binet 公式的求法。轮回方阵本身不可能写成两个矩阵的乘积，但是如果我们另设一个矩阵，两个矩阵乘积可以写成和一个对角矩阵的乘积，而对角矩阵的行列式是非常容易得到的，从而就可以得到轮回方阵的行列式。与其类似的文献[4]第三章第二节习题第4题的第(4)小题，采用同样的处理方法就可以得到结果。

**Question 4**.$^{[4]}$ $n$ 阶方阵
$$
\begin{pmatrix}
a_0 & a_1 & a_2 & \cdots & a_{n-1} \\
a_{n-1} & a_0 & a_1 & \cdots & a_{n-2} \\
a_{n-2} & a_{n-1} & a_0 & \cdots & a_{n-3} \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
a_1 & a_2 & a_3 & \cdots & a_0
\end{pmatrix}.
$$
称为轮回方阵，求 $n$ 阶轮回方阵的行列式。

**Solution**. 设 $\omega$ 是 $n$ 次本原单位根，即 $\omega^i\neq 1,1\le i\le n-1,\omega^n=1$，$f(x)=a_0+a_1x+\cdots+a_{n-1}x^{n-1}$，取 $n$ 阶矩阵 $B$ 为
$$
B=\begin{pmatrix}
1 & 1 & 1 & \cdots & 1 \\
1 & \omega & \omega^2 & \cdots & \omega^{n-1} \\
1 & \omega^2 & \omega^4 & \cdots & \omega^{2(n-1)} \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
1 & \omega^{n-1} & \omega{2(n-1)} & \cdots & \omega{(n-1)^2}
\end{pmatrix}
$$
容易验证 $AB=Bdiag(f(1), f(\omega), f(\omega^2), \cdots, f(\omega^{n-1}))$. 两端各取行列式，则由
$$
det Adet B=\left(\prod_{i=0}^{n-1}f(\omega^i)\right)detB.
$$
显然 Vandermonde 行列式 $detB=\displaystyle\prod_{1\le i<j\le n}(\omega^j-\omega^i)\neq 0$. 因此 $detA=\displaystyle\prod_{i=0}^{n-1}f(\omega^i)$.

## Binet-Cauchy 在数学分析中的应用

最近几天在复习数学分析中隐函数组的内容，在华东师范版数学分析下册第十八章隐函数组这一节中，有这么一道课后习题，它直接体现了Cauchy-Binet 公式的结论。题目叙述如下:

**Question5**. 设 $u=u(x,y,z),v=v(x,y)$ 和 $x=x(s,t),y=y(s,t),z=z(s,t)$ 都有连续的一阶偏导数，证明
$$
\frac{\partial (u,v)}{\partial (s,t)}=\frac{\partial (u,v)}{\partial (x,y)}\frac{\partial (x,y)}{\partial (s,t)}+\frac{\partial (u,v)}{\partial (y,z)}\frac{\partial (y,z)}{\partial (s,t)}+\frac{\partial (u,v)}{\partial (z,x)}\frac{\partial (z,x)}{\partial (s,t)}.
$$

对于这么一道题，首先需要求出 $u_s,u_t,v_s,v_t$, 然后按照公式一步步计算即可，这是最基本的思路。注意到要证明的恒等式是关于 Jacobi 行列式的，所以也可以使用行列式的技巧进行简化计算，即通过行列式的性质进行拆分，可以得到9个行列式，其中3个为0，剩余6个两两组合即可得到待着证结论，具体过程就不再详细写出。更进一步，左边的行列式可以写成一个 $2\times 3$ 的矩阵和一个 $3\times 2$ 的矩阵的乘积，这就联系到了 Cauchy-Binet 公式，应用前面所叙述的，直接就可以得到这个式子成立。即

**Proof.** 首先由复合函数求偏导的链式法则得
$$
u_s=u_xx_s+u_yy_s+u_zz_s, u_t=u_xx_t+u_yy_t+u_zz_t, \\
v_s=v_xx_s+v_yy_s+v_zz_s, v_t=v_xx_t+v_yy_t+v_zz_t.
$$
即
$$
\begin{pmatrix}
u_s & u_t \\
v_s & v_t
\end{pmatrix}=\begin{pmatrix}
u_x & u_y & u_z \\
v_x & v_y & v_z
\end{pmatrix}\begin{pmatrix}
x_s & x_t \\
y_s & y_t \\
z_s & z_t
\end{pmatrix}
$$
所以根据 Cauchy-Binet 公式，
$$
\begin{aligned}
&\begin{vmatrix}
u_s & u_t \\
v_s & v_t
\end{vmatrix}=\begin{vmatrix}\begin{pmatrix}
u_x & u_y & u_z \\
v_x & v_y & v_z
\end{pmatrix}\begin{pmatrix}
x_s & x_t \\
y_s & y_t \\
z_s & z_t
\end{pmatrix}\end{vmatrix} \\
=&\begin{vmatrix}
u_x & u_y \\
v_x & v_y 
\end{vmatrix}\begin{vmatrix}
x_s & x_t \\
y_s & y_t
\end{vmatrix}+\begin{vmatrix}
u_x & u_z \\
v_x & v_z 
\end{vmatrix}\begin{vmatrix}
x_s & x_t \\
z_s & z_t 
\end{vmatrix}+\begin{vmatrix}
u_y & u_z \\
v_y & v_z 
\end{vmatrix}\begin{vmatrix}
y_s & y_t \\
z_s & z_t
\end{vmatrix}.\end{aligned}
$$

## 参考文献

[1] 姚穆生,吴泉水.高等代数学[M].上海:复旦大学出版社.2007.

[2] 李维伦.Binet-Cauchy公式及其应用[J].工科数学,2002,3.

[3] 王斌儒,刘延卿.Binet-Cauchy公式及其应用[J].科技风,2018,9.

[4] 李炯生,查建国,王新茂.线性代数[M].合肥:中国科学技术大学出版社.2010.

[5] 李傅山,王培合.数学分析习题课讲义3[M].北京:北京大学出版社.2018,10.
