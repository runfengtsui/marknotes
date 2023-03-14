---
Title: Python绘制三维图像实例
Author: 邱彼郑楠
Date: 2020-08-09
Modified: 2022-05-18
Category: Python
Tags: Matplotlib
Slug: python-matplitlib-3d
---

Python 的 Matplotlib 库是一个比较强大的绘图库，可以比较好的代替 Matlab 实现绘图功能。下面我从学校开设的 Matlab 上机实验课程中的练习题挑出与绘图相关的练习给出  Python 代码，仅供参考。

Matplotlib 库通常用来绘制二维曲面图形，下面我们给出了二维曲线的一个标记的例子和一个绘制子图的例子；其余的例子都是绘制三维图形，这需要将坐标轴设置为三维的坐标系，我们主要采用下列方式进行设置：

```python
fig = plt.figure()
ax = fig.subplot(111, projection='3d')
```

另外一种方式需要调用 Matplotlib 库的一个工具包，可以自行网上搜索进行学习。

## 示例一 曲线的标记

> 绘出函数 $y=3\cos x e^{\sin x}$ 在 $[0,5]$ 上黑色实型曲线图，线宽为 3，数据点用圆圈标记的，尺寸为 6，标记点的边缘颜色为红色，标记点的填充颜色为绿色；加栅阁并且绘图区域为正方形，各坐标轴采用登场刻度。

```python
import matplotlib.pyplot as plt
import numpy as np


if __name__ == '__main__':
    x = np.arange(0, 5, 0.1)
    y = 3*np.cos(x)*np.exp(np.sin(x))
    fig, ax = plt.subplots()
    ax.plot(x, y, 'k-o', linewidth=3,
           markeredgecolor='r',
           markerfacecolor='g',
           markersize=10)
    ax.grid(True)
    plt.axis('equal')
    plt.show()

```

绘制的图形如下图所示：

<div style="text-align: center;">
<img src="https://kristophertsui.gitee.io/figure/imgs/curve_markers.png" alt="curveMarker" title="Curve Marker">
</div>

## 示例二 参数方程

> 绘制曲线 $\begin{cases} x = 2(\cos t + t\sin t) \\ y = 2(\sin t - t\cos t) \\ z=1.5t \end{cases}$，$t$ 的变化范围为 $[0, 10\pi]$.

```python
import matplotlib.pyplot as plt
import numpy as np


if __name__ == '__main__':
    t = np.arange(0, 10*np.pi, 0.1*np.pi)
    x = 2*(np.cos(t) + t*np.sin(t))
    y = 2*(np.sin(t) - t*np.cos(t))
    z = 1.5*t
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    ax.plot3D(x, y, z)
    plt.show()

```

`plot3D()`是用来绘制三维曲线的，类似于`plot()`函数。绘制的图形如下图所示：

<div style="text-align: center">
<img src="https://kristophertsui.gitee.io/figure/imgs/parametric_equation.png" alt="parametric equation" title="parametric equaiton">
</div>

> 绘制环面图形，其参数方程为：
> $$
> \begin{cases}
> x = (2 + \cos u)\cos v \\
> y = (2 + \cos u)\sin v \\
> z = \sin u
> \end{cases} \quad\quad\quad u\in[0,2\pi],v\in[0,2\pi]
> $$

```python
import matplotlib.pyplot as plt
import numpy as np


if __name__ == '__main__':
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    u, v = np.mgrid[0:2*np.pi:40j, 0:2*np.pi:40j]
    x = (2 + np.cos(u))*np.cos(v)
    y = (2 + np.cos(u))*np.sin(v)
    z = np.sin(u)
    ax.plot_surface(x, y, z, rstride=1, cstride=1)
    plt.show()

```

`plot_surface()`和Matlab中的`surf()`比较相似，是用来绘制三维曲面的，后面的**rstride**和**cstride**这两个参数分别表示行之间的跨度和列之间的跨度；和这两个不能同时出现的是**rcount**和**ccount**，分别表示行的间隔个数和列的间隔个数；另外还有**cmap**参数，可以设置颜色。绘制的图形图下图所示：

<center>
<img src="https://kristophertsui.gitee.io/figure/imgs/torus.png" alt="torus">
</center>

## 示例三 子图的绘制

> 在 $[0,30]$ 内分别绘出下列函数的图像(采样点均为100个)：$y=\sin x$，$y=x\sin x$，$y=x\sin^2 x$，$y=x^2 \sin^2 x$，使得四个图像分别按左上，左下，右上，右下的顺序在同一窗口中排列，并对每一个图形分别加以标注，指明该曲线所表示的函数。

```python
import matplotlib.pyplot as plt
import numpy as np


if __name__ == '__main__':
    x = np.linspace(0, 30, 100)
    fig = plt.figure()
    ax1 = fig.add_subplot(221)
    ax1.plot(x, np.sin(x))
    ax1.set_title(r'$\sin(x)$')
    ax2 = fig.add_subplot(222)
    ax2.plot(x, x*np.sin(x)*np.sin(x))
    ax2.set_title(r'$x\sin^2(x)$')
    ax3 = fig.add_subplot(223)
    ax3.plot(x, x*np.sin(x))
    ax3.set_title(r'$x\sin(x)$')
    ax4 = fig.add_subplot(224)
    ax4.plot(x, x*x*np.sin(x)*np.sin(x))
    ax4.set_title(r'$x^2\sin^2(x)$')
    plt.show()

```

在设定标签时如果要支持 LaTeX 语法，需要使用`r'$$'`字符串，这一点和 Matlab 不同。绘制的图形如下图所示：

<center>
<img src="https://kristophertsui.gitee.io/figure/imgs/subplots.png" alt="subplots">
</center>

## 示例四 曲面的绘制

> 画出下列方程式的曲面图
> $$
> f(x,y) = 0.2\cos x + y\exp(-x^2 - y^2)
> $$
> 其中，$x$ 的21个值均匀分布在 $[-2\pi, 2\pi]$ 范围，$y$ 的31个值均匀分布在 $[-\pi, \pi]$。并对点 $(0,0,f(0,0))$ 用箭头进行标注。

```python
import matplotlib.pyplot as plt
import numpy as np


if __name__ == '__main__':
    x = np.linspace(-2*np.pi, 2*np.pi, 21)
    y = np.linspace(-np.pi, np.pi, 31)
    X, Y = np.meshgrid(x, y)
    f = lambda x, y: 0.2*np.cos(x) + y*np.exp(-x*x - y*y)
    Z = f(X, Y)
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    ax.plot_wireframe(X, Y, Z, rstride=1, cstride=1)
    ax.text(0, 0, f(0, 0), 
            r'$\leftarrow(0,0,' + str(f(0, 0)) + ')',
            zdir=(-1, -1, 0))
    plt.show()

```

这里使用箭头标记不能使用`annotate()`函数，因为这个函数中`xy`坐标只能是二维坐标。使用`text()`进行标记和Matlab中的差不多，箭头使用的LaTeX语法，另外`zdir`参数是标记文字的方向。绘制好的图形如下图所示：

<center>
<img src="https://kristophertsui.gitee.io/figure/imgs/arrow.png" alt="arrow">
</center>

> 绘制 $z = x_1^4 + 3x_1^2 + x_2^2 -2x_1 - 2x_2 -2x_1^2x_2  +6$ 的三维图形，其中 $x_1\in[-3,3]$，$x_2\in[-3,13]$。

```python
import numpy as np
import matplotlib.pyplot as plt


if __name__ == '__main__':
    x1 = np.arange(-3, 3, 0.1)
    x2 = np.arange(-3, 13, 0.5)
    X, Y = np.meshgrid(x1, x2)
    Z = X**4 + 2X**2 + Y**2 - 2*X - 2*Y - 2*X**2*Y + 6
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    ax.plot_surface(X, Y, Z, rstride=1, cstride=1, cmap='rainbow')

```

绘制的图形如下图所示：

<center>
<img src="https://kristophertsui.gitee.io/figure/imgs/surface.png" alt="surface">
</center>

## 示例五 多个图形的绘制

> 在同一个图形窗口内绘制：窗口半径为2的球面，$z=4$ 的平面及墨西哥帽子函数：$z = \dfrac{\sin\sqrt{x^2 + y^2}}{\sqrt{x^2 + y^2}}$.

```python
import matplotlib.pyplot as plt
import numpy as np


if __name__ == '__main__':
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    # 绘制窗口半径为2的球面
    phi, theta = np.mgrid[0:2*np.pi:40j, 0:np.pi:20j]
    x = 2*np.sin(phi)*np.cos(theta)
    y = 2*np.sin(phi)*np.sin(theta)
    z = 2*np.cos(phi)
    ax.plot_surface(x, y, z, rstride=1, cstride=1, cmap='rainbow')
    # 绘制z=4的平面
    x = np.arange(-2, 2, 0.2)
    y = np.arange(-2, 2, 0.2)
    X, Y = np.meshgrid(x, y)
    ax.plot_surface(X, Y, 4*np.one_like(X),
                   rstride=1, cstride=1, cmap='rainbow')
    # 绘制墨西哥帽子函数
    x = np.arange(-4.1, 4.1, 0.2)
    y = np.arange(-4.1, 4.1, 0.2)
    X, Y = np.meshgrid(x, y)
    Z = np.sin((X**2 + Y**2)**0.5)/(X**2 + Y**2)**0.5
    ax.plot_surface(X, Y, Z, rstride=1, cstride=1)
   	plt.show()

```

球面、柱面这些三维图形不像Matlab中有直接的函数进行绘制，比较好的方法就是通过参数方程来解决。另外，`mgrid()`函数中的`j`表示个数，这里不需要使用`hold`来保持不动，可以直接绘制多个图形。**值得注意的是**，在绘制墨西哥帽子函数时，参数的取值不能有0，否则会出现无穷大的情况报错。绘制好的图形如下图所示：

<center>
<img src="https://kristophertsui.gitee.io/figure/imgs/multisurfaces.png" alt="multisurfaces">
</center>

## 示例六 旋转抛物面

> 绘制一个旋转抛物面 $z = \dfrac{x^2 + y^2}{60}$.

```python
import numpy  as np
import matplotlib.pyplot as plt


if __name__ == '__main__':
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    rho, theta = np.mgrid[0:np.sqrt(60):60j, 0:2*np.pi:40j]
    x = rho*np.cos(theta)
    y = rho*np.sin(theta)
    z = rho**2/60
    ax.plot_surface(x, y, z, rstride=1, cstride=1)
	plt.show()

```

绘制的图形如下图所示：

<center>
<img src="https://kristophertsui.gitee.io/figure/imgs/paraboloid_revolution.png" alt="paraboloid revolution">
</center>

## 示例七 圆柱面

>绘制圆柱面 $x^2 + y^2 = x$.

```python
import matplotlib.pyplot as plt
import numpy as np


if __name__ == '__main__':
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    h = np.linspace(0, 1, 20)
    theta = np.linspace(0, 2*np.pi, 40)
    x = np.outer(np.sin(theta), np.ones(len(h)))
    y = np.outer(np.cos(theta), np.ones(len(h)))
    z = np.outer(np.ones(len(theta)), h)
    ax.plot_surface(x+0.5, y, z, rstride=1, cstride=1)
    plt.show()

```

绘制圆柱的时候各坐标均是由向量的外积进行计算的，毕竟竖坐标不受横纵坐标的影响。绘制好的图形如下图所示：

<center>
<img src="https://kristophertsui.gitee.io/figure/imgs/cylindrical.png" alt="cylindrical">
</center>

> 绘制圆柱面 $x^2 + y^2 = 1$ 的图像，高度范围在 $[-2, 2]$

```python
import matplotlib.pyplot as plt
import numpy as np


if __name__ == '__main__':
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    h = np.linspace(-2, 2, 80)
    theta = np.linspace(0, 2*np.pi, 40)
    x = np.outer(np.sin(theta), np.ones(len(h)))
    y = np.outer(np.cos(theta), np.ones(len(h)))
    z = np.outer(np.ones(len(theta)), h)
    ax = plot_surface(x, y, z, rstride=1, cstride=1)
    plt.show()

```

绘制好的图形如下图所示：

<center>
<img src="https://kristophertsui.gitee.io/figure/imgs/cylindrical_height.png" alt="cylindrical with height">
</center>

## 示例八 圆锥面

> 绘制圆锥面 $\begin{cases} x = u\sin v \\ y = u\cos v \\ z = u \end{cases}$参数 $u$ 的范围是 $[-2, 2]$，$v$ 的范围是 $[0, 2\pi]$.

```python
import matplotlib.pyplot as plt
import numpy as np


if __name__ == '__main__':
	fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    u, v = np.mgrid[-2:2:80j, 0:2*np.pi:40j]
    x = u*np.sin(v)
    y = u*np.cos(v)
    z = u
    ax.plot_surface(x, y, z, rstrid=1, cstride=1)
    plt.show()

```

绘制好的图形如下图所示：

<center>
<img src="https://kristophertsui.gitee.io/figure/imgs/cone.png" alt="cone">
</center>

Matplotlib 库有很多其他的应用，这里面所说的内容还不完全，有待补充。
