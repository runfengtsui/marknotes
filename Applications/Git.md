---
Title: Git 使用教程
Author: 邱彼郑楠
Date: 2022-11-06
Modified: 2023-05-27
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

忽略 filemode 的变化[^filemode]

```git
git config --add core.filemode false
```

# 分支操作
## 空分支的创建

如果想要创建一个新的分支, 可以使用 `git checkout -b newbranch` 命令, 然后使用 `git checkout branchname` 命令可以在分支间切换.

但是这样创建的分支非空. 如果想要创建一个空分支, 则需要使用 `git checkout -orphan emptybranch` 命令[^emptybranch]. 该命令创建的分支不承接之前所有的提交, 此时使用 `git rm -rf .` 命令清除内容, 就得到了一个空分支. 空分支在不提交任何内容的情况下, `git branch` 命令是不显示该分支的. 可以添加一个 `README.md` 文件描述提交, 这样就可以看见新分支了.


## 克隆远程分支
### 单分支的克隆

想要将远程仓库的一个分支克隆到本地, 只需要增加 `-b` 参数:

```git
git clone -b branchname git@gitee.com:username/repositoryname.git
```

### 所有分支的克隆

使用 `git clone` 克隆远程仓库只包含主分支, 其他分支是不会被克隆到本地的.

如果想要把远程仓库的所有分支都克隆到本地, 首先需要在本地也建立相应的分支. 即

```git
git checkout -b branchname origin/branchname
```

这样就把远程仓库的 `branchname` 分支克隆到本地了. 参考 [怎么用git clone 远程的所有分支](https://www.jianshu.com/p/0fe715a7fbb3).

## 重命名
### 本地分支

本地分支在没有推送到远程的情况下, 只需要使用以下命令:

```git
git branch -m oldname newname
```

### 远程分支

如果本地分支已经推送到了远程仓库中, 则除了上述命令更改本地的分支名之外, 还需要更改远程仓库的分支名.

首先, 需要删除远程分支

```git
git push --delete origin oldname
```

然后将新命名的本地分支推送到远程仓库

```git
git push origin newname
```

最后, 把修改后的本地分支与远程分支关联

```git
git branch --set-upstream-to origin/newname
```

详细请参考 [git分支怎样改名字](https://www.php.cn/tool/git/487573.html).

[^emptybranch]: Geometryolife.[如何快速在 Git 中创建一个空分支（孤立分支）](https://zhuanlan.zhihu.com/p/453126177)[OL].(2022-1-4)[2023-5-19].
[^filemode]: lxw1844912514.[git diff提示filemode发生改变（old mode 100644、new mode 10075）](https://blog.csdn.net/lxw1844912514/article/details/103418431)[OL].(2019-12-6)[2023-5-27].

