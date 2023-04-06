---
Title: Git 使用教程
Author: 邱彼郑楠
Date: 2022-11-06
Modified: 2023-04-06
---

# 设置
## 初始设置

首先设置使用 Git 时的姓名和邮箱地址,

```git
git config --global user.name "name"
git config --global user.email "email@email.com"
```

该设置会保存在 `~/.gitconfig` 设置文件中.

## 其他设置

修改默认主分支名称：

```git
git config --global init.defaultBranch <name>
```

# 分支操作

如果想要创建一个新的分支, 可以使用 `git checkout -b newbranch` 命令, 然后使用 `git checkout branchname` 命令可以在分支间切换.

但是这样创建的分支非空. 如果想要创建一个空分支, 则需要使用 `git checkout -orphan emptybranch` 命令. 该命令创建的分支不承接之前所有的提交, 此时使用 `git rm -rf .` 命令清除内容, 就得到了一个空分支. 空分支在不提交任何内容的情况下, `git branch` 命令是不显示该分支的. 可以添加一个 `README.md` 文件描述提交, 这样就可以看见新分支了.

参考 [如何快速在 Git 中创建一个空分支（孤立分支）](https://zhuanlan.zhihu.com/p/453126177#:~:text=%E5%88%9B%E5%BB%BA%E5%AD%A4%E7%AB%8B%EF%BC%88%E7%A9%BA%EF%BC%89%E5%88%86%E6%94%AF%20%E4%BD%BF%E7%94%A8%20git%20checkout%20-b%20%E5%91%BD%E4%BB%A4%E5%88%9B%E5%BB%BA%E7%9A%84%E5%88%86%E6%94%AF%E6%98%AF%E6%9C%89%E7%88%B6%E8%8A%82%E7%82%B9%E7%9A%84%EF%BC%8C%E8%BF%99%E6%84%8F%E5%91%B3%E7%9D%80%E6%96%B0%E7%9A%84%E5%88%86%E6%94%AF%E5%8C%85%E5%90%AB%E4%BA%86%E5%8E%86%E5%8F%B2%E6%8F%90%E4%BA%A4%EF%BC%8C%E6%89%80%E4%BB%A5%E6%88%91%E4%BB%AC%E9%9C%80%E8%A6%81%E4%BD%BF%E7%94%A8%20git%20checkout,Output%20%3D%3D%3D%20Switched%20to%20a%20new%20branch%20%27img%27).
