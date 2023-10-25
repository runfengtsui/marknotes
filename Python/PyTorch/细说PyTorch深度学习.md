---
title: 细说PyTorch深度学习
Author: 邱彼郑楠
Date: 2023-08-21
Modified: 2023-08-24
---

# 版权信息

| 书名     | 细说PyTorch深度学习: 理论、算法、模型与编程实现 |
|----------|-------------------------------------------------|
| 作者     | 凌峰, 丁麒文                                    |
| 出版社   | 清华大学出版社                                  |
| 出版时间 | 2023-06-01                                      |
| ISBN     | 9787302631941                                   |

# 人工智能

**人工智能**是计算机学科的一个分支, 是研究, 开发用于模拟, 延伸和拓展人的智能的理论, 方法, 技术及应用系统的一门新的技术科学.

当今没有统一的原理或范式指导人工智能研究, 在许多问题上研究者都存在争论:
- 是否应从心理或神经方面模拟人工智能, 或者像鸟类生物学对于航空工程一样, 人类生物学与人工智能研究是没有关系的
- 智能行为能否用简单的原则(如逻辑或优化)来描述, 还是必须解决大量无关的问题

# 开发环境
## NumPy

- `numpy.array(object, dtype=None, copy=True, order=None, subok=False, ndmin=0)`

| 参数   | 描述                                                       |
|--------|------------------------------------------------------------|
| object | 数组或嵌套的数列                                           |
| dtype  | 数组元素的数据类型, 可选                                   |
| copy   | 对象是否需要复制, 可选                                     |
| order  | 创建数组的样式, C 为行方向, F 为列方向, A 为任意方向(默认) |
| subok  | 默认返回一个与基类类型一致的数组                           |
| ndmin  | 指定生成数组的最小维度                                     |

- `numpy.empty` 方法用来创建一个指定形状 (shape), 数据类型 (dtype) 且未初始化的数组:

```python
numpy.empty(shape, dtype=float, order='C')
```

- `numpy.zeros` 创建指定大小的数组, 数组元素以 0 来填充.

```python
numpy.zeros(shape, dtype=float, order='C')
```

- `numpy.ones` 创建指定形状的数组, 数组元素以 1 来填充.

```python
numpy.ones(shape, dtype=None, order='C')
```

- `numpy.asarray` 类似于 `numpy.array`.

```python
numpy.asarray(a, dtype=None, order=None)
```

其中 `a` 是任意形式的输入参数, 可以是列表, 列表的元组, 元组, 元组的元组, 元组的列表, 多维数组.

- `numpy.frombuffer` 用于实现动态数组.

`numpy.frombuffer` 接收 `buffer` 输入的参数, 以流的形式读入并转化成 `ndarray` 对象. `buffer` 是字符串时, Python 3 默认 `str` 是 Unicode 类型, 所以要转成 `bytestring`, 在原 `str` 前加上 `b`.

```python
numpy.frombuffer(buffer, dtype=float, count=-1, offset=0)
```

其中 `count` 为读取的数据数量, 默认为 -1, 读取所有数据. `offset` 为读取的起始位置, 默认为 0. 

- `numpy.fromiter` 方法可从迭代对象中建立 `ndarray` 对象, 返回一维数组.



