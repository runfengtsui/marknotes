---
Title: High precision aerodynamic heat prediction method based on data augmentation and transfer learning
Author: 邱彼郑楠 (runfengtsui@yeah.net)
Date: 2025-02-23 11:35:43
Modified: 2025-02-23 11:35:43
---

> **题目:** High precision aerodynamic heat prediction method based on data augmentation and transfer learning 
>
> **作者信息:** 西北工业大学 张伟伟等
>
> **期刊:** Aerospace Science and Technology

# 数据增强 (Data Augmentation)

> 数据扩充是指从原始数据中合成新的数据, 或者加入与原始数据类型不同的其他数据, 以达到数据扩充的目标.
>
> * B. Li, Y. Hou, W. Che, Data augmentation approaches in natural language processing: a survey, AI Open 3 (2021).
> * C. Shorten, T. M. Khoshgoftaar, A survey on image data augmentation for deep learning, J. Big Data 6 (2019).
> * C. Shorten, T. M. Khoshgoftaar, and B. Furht, Text data augmentation for deep learning, J. Big Data 8 (2021).

作者对高精度气动热风洞实验数据进行数据扩充, 并基于扩充数据构建数据驱动的气动热预测模型.

# 迁移学习 (Transfer Learning)

> 一种通过将从特定源领域获得的知识应用到新的目标领域来提高模型在目标领域性能的有效的技术.
>
> * S. J. Pan, Q. Yang, A survey on transfer learning, IEEE Trans Knowl. Data Eng. 22 (2010) 1345.
> * C. tan, F. Sun T. Kong, W. Zhang, C. Yang, C. Liu, A Survey on Deep transfer Learning (2018). Rhodes, GREECE.
> * F. Zhuang, Z. Qi, K. Duan, D. Xi, Y. Zhu, H. Zhu, H. Xiong, Q. He, A comprehensive survey on transfer learning, Proc. IEEE 109 (2021) 43.

作者采用迁移学习的方法, 利用很少的新形状飞机的气动热风洞实验数据对原始数据驱动的气动热预测模型进行了微调, 从而可以准确预测新型飞机的空气动力热分布.

# 创新点

传统的数据驱动的气动热预测模型简单有效, 但需要大量样本且缺乏形状泛化能力, 即使结合数据扩充和迁移学习技术, 性能也不达标.

作者基于边界层外缘与壁面气动热之间的物理关系, 提出一种数据驱动的气动热模型 ED-ResNet. (这应该算是一种物理信息神经网络)
