---
Title: Git 使用教程
Author: 邱彼郑楠
Date: 2022-11-06
Modified: 2023-07-16
---
[toc]
# 配置
## 初始配置

安装完成后, 需要进行一部设置, 在命令行输入:

```git
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

因为 Git 是**分布式版本控制系统**, 所以, 每个及其都必须自报家门:你的名字和Email地址. 

注意 `git config` 命令的 `--global` 参数, 用了这个参数, 表示你这台机器上所有的 Git 仓库都会使用这个配置, 当然也可以对某个仓库指定不同的用户名和 Email 地址. 

## 其他配置

修改默认主分支名称:

```git
git config --global init.defaultBranch <name>
```

忽略 filemode 的变化[^filemode]
[^filemode]: lxw1844912514.[git diff提示filemode发生改变（old mode 100644、new mode 10075）](https://blog.csdn.net/lxw1844912514/article/details/103418431)[OL].(2019-12-6)[2023-5-27].

```git
git config --add core.filemode false
```

# 创建版本库

版本库又名仓库, 英文名 repository, 可以简单理解成一个目录, 这个目录里面的所有文件都可以被 Git 管理起来, 每个文件的修改、删除、Git 都能跟踪, 以便任何时刻都可以追踪历史, 或者在将来每个时刻可以“ 还原” . 

所以, 创建一个版本库非常简单, 首先, 选择一个合适的地方, 创建一个空目录:

```bash
$ mkdir learngit
$ cd learngit
$ pwd
E:\learngit
```

`pwd` 命令用于显示当前目录. 以此为例, 这个仓库位于 `E:\learngit`.

第二步, 通过 `git init` 命令把这个目录变成 Git 可以管理的仓库:

```git
$ git init
Initialized empty Git repository in E:/learngit/.git/
```

瞬间 Git 就把仓库建好了, 而且告诉你是一个空的仓库（empty Git repository）. 同时当前目录下多了一个 `.git` 的目录, 这个目录是 Git 来跟踪管理版本库的, **不要手动修改这个目录里面的文件**, 如果改乱了, GIt 仓库就被破坏了. 

如果没有找到 `.git` 目录, 那是因为这个目录默认是隐藏的, 用 `ls -ah`命令就可以看见. 另外, 也不一定必须在空目录下创建 Git 仓库, 选择一个已经有东西的目录也是可以的. 

# 把文件添加到版本库

所有的版本控制系统, 其实只能跟踪**文本文件**的改动, 比如 TXT 文件, 网页, 所有的程序代码等等, Git 也不例外. 版本控制系统可以告诉你每次的改动, 比如在第5行加了一个单词“Linux”, 在第8行删了一个单词“Windows”. 而图片、视频这些**二进制文件**, 虽然也能由版本控制系统管理, 但无法跟踪文件的变化, 只能把二进制文件每次改动串起来, 也就是只知道图片从100KB改成了120KB, 但到底做了怎样的改动, 版本控制系统不知道, 也没法知道.

Microsoft 的 Word 格式是二进制格式, 因此, 版本控制系统是无法跟踪 Word 文件的改动的, 前面我们举的例子只是为了演示, 如果要真正使用版本控制系统, 就要以纯文本方式编写文件.

现在, 我们编写一个 `readme.txt` 文件, 内容如下:

```
Git is a version control system.
GIt is free software.
```

一定要放在 `learngit` 目录下（子目录也行）, 因为这是一个 Git 仓库, 放到其他地方 Git 再厉害也找不到这个文件. 把一个文件放到 Git 仓库只需要两步.

* 第一步, 用命令 `git add` 告诉 Git, 把文件添加到仓库:

```git
$ git add .\readme.txt
```

执行上面的命令, 没有任何的显示, 这就对了, Unix 的哲学是”没有消息就是好消息“, 说明添加成功.

* 第二步, 用命令 `git commit` 告诉 Git, 把文件提交到仓库:

```git
$ git commit -m "wrote a readme file"
[master (root-commit) bbd5bce] wrote a readme file
 1 file changed, 2 insertionss(+)
 creat mode 100633 readme.txt
```

`git commit` 命令, `-m` 后面输入的是本次提交的说明, 可以输入任何内容, 当然最好是有意义的, 这样你就能从历史记录里方便地找到改动记录.

`git commit` 民工执行成功后会告诉你, `1file changed` :1个文件被改动（我们新添加的 readme.txt 文件）；`1 file changed`:1个文件被改动（我们新添加的 readme.txt 文件）；`2 insertions`:插入了两行内容(reaadme.txt 有两行内容).

为什么 Git 添加文件需要 `add`, `commit` 一共两步呢？因为 `commit` 可以一次提交很多文件, 所以你可以多次 `add` 不同的文件, 比如:

```git
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files"
```

## 时光机穿梭

我们已经成功地添加并提交了一个 readme.txt 文件, 现在, 是时候继续工作了. 于是, 我们继续修改readme.txt 文件, 改成如下内容:

```
Git is a distributed version control system.
Git is free software.
```

现在, 运行 `git status` 命令查看结果

```git
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   readme.txt

no changes add to commit (use "git add" and/or "git commit -a")
```

`git status` 命令可以让我们时刻掌握仓库的当前状态, 上面的命令输出告诉我们, `readme.txt` 被修改过了, 但还没有准备提交的修改.

虽然 Git 告诉我们 `readme.txt` 被修改了, 但如果能看看具体修改了什么内容, 自然是很好的. 如果记不清上次怎么修改的 `readme.txt`, 需要用 `git diff` 这个命令看看:

```git
$ git diff readme.txt
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is a free software.
```

`git diff` 顾名思义就是查看 difference, 显示的格式是 Unix 通用的 diff 格式, 可以从上面的命令输出看到, 我们在第一行添加了一个 distributed 单词.

知道了对 `readme.txt` 做了什么修改后, 再把它提交到仓库就放心多了, 提交修改和提交新文件是一样的两步, 第一步是 `git add`:

```git
$ git add readme.txt
```

同样没有输出. 在执行第二步 `git commit` 之前, 我们再运行 `git status` 看看当前仓库的状态:

```git
$ git status
On branch master
Changes to be committed
  (use "git restore --staged <file>..." to unstage)
  modified:   readme.txt

```

`git status` 告诉我们, 将要提交的修改包括 `readme.txt`, 下一步, 既可以放心地提交了:

```git
$ git commit -m "add distributed"
[master 2937c15] add distributed
 1 file changed, 1 insertion(+), 1 deletion(-)
```

提交后, 我们再用 `git status` 命令查看仓库的当前状态:

```git
$ git status
On branch master
nothing to commit, working tree clean
```

Git 告诉我们当前没有需要提交的修改, 而且, 工作目录是干净的(working tree clean).

## 版本回退

修改 readme.txt 文件如下:

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
```

然后尝试提交:

```git
$ git add readme.txt
$ git commit -m "append GPL"
[master d95c9ac] append GPL
 1 file changed, 1 insertion(+), 1 deletion(-)
```

像这样, 你不断对文件进行修改, 然后不断提交修改到版本库里, 就好比玩RPG游戏时, 每通过一关就会自动把游戏状态存盘, 如果某一关没过去, 你还可以选择读取前一关的状态. 有些时候, 在打 Boss 之前, 你会手动存盘, 以便万一打 Boss 失败了, 可以从最近的地方重新开始. Git也是一样, 每当你觉得文件修改到一定程度的时候, 就可以保存一个快照, 这个快照在 Git 中被称为 `commit` . 一旦你把文件改乱了, 或者误删了文件, 还可以从最近的一个 `commit` 恢复, 然后继续工作, 而不是把几个月的工作成果全部丢失.

现在我们回顾以下 `readme.txt` 文件一共有几个版本被提交到 Git 仓库里了:

* 版本1:wrote a readme file

```
Git is a version control system.
Git is free software.
```

* 版本2:add distributed

```
Git is a distributed version control system.
Git is free software.
```

* 版本3:append GPL

```
Git is a distributed version control system.
Git is free software distributed undeer the GPL.
```

当然, 在实际工作中, 我们不可能记住一个几千行的文件每次都改了什么内容, 不然要版本控制系统干什么. 版本控制系统可定有某个命令可以告诉我们历史纪录, 在 Git 中, 我们用 `git log` 命令查看:

```git
$ git log
commit d95c9ac1905470961c5ad29b445afff648971661 (HEAD -> master)
Author: Tsui <kristophertsui@163.com>
Date:   Sat Dec 7 20:23:19 2019 +0800

    append GPL

commit 2937c152b91a09c5a723fce2d88d5a86d3f584ce
Author: Tsui <kristophertsui@163.com>
Date:   Sat Dec 7 20:17:10 2019 +0800

    add distributed

commit bbd5bcef700db0f55d1f8c77b9a13fad6dc38abc
Author: Tsui <kristophertsui@163.com>
Date:   Sat Dec 7 20:09:08 2019 +0800

    wrote a readme file
```

`git log` 命令显示的是从最近到最远的提交日志, 我们可以看到3次提交, 最近的一次是 `append GPL`, 上一次是 `add distributed`,最早的一次是 `wrote a readme file`.

如果嫌输出的信息太多, 看得眼花缭乱的, 可以试试加上 `--pretty=oneline` 参数:

```git 
$ git log --pretty=oneline
d95c9ac1905470961c5ad29b445afff648971661 (HEAD -> master) append GPL
2937c152b91a09c5a723fce2d88d5a86d3f584ce add distributed
bbd5bcef700db0f55d1f8c77b9a13fad6dc38abc wrote a readme file
```

需要提示的是, 你看到的一大串类似 `d95c9ac...` 的是 `commit id`（版本号）, 和 SVN 不一样, Git 的 `commit id` 不是1, 2, 3......递增的数字, 而是一个 SHA1 计算出来的一个非常大的数字, 用十六进制表示, 而且你看到的 `commit id` 和我的肯定不一样, 以你自己的为准. 为什么 `commit id` 需要用这么一大串数字表示呢？因为 Git 是分布式的版本控制系统, 后面我们还要研究多人在同一个版本库里工作, 如果大家都用1, 2, 3......作为版本号, 那肯定就冲突了.

每提交一个新版本, 实际上 Git 就会把它们自动串成一条时间线. 如果使用可视化工具查看 Git 历史, 就可以更清楚地看到提交历史的时间线:

![alt 历史](https://static.liaoxuefeng.com/files/attachments/919019707114272/0)

好了, 现在我们启动时光穿梭机, 准备把 `readme.txt` 回退到上一个版本, 也就是 `add distributed` 的那个版本, 怎么做呢?

首先, Git 必须知道当前版本是哪个版本, 在 Git 中, 用 `HEAD` 表示当前版本, 也就是最新的提交 `d95c0ac...` , 上一个版本就是 `HEAD^` , 上上一个版本就是 `HEAD^^`, 当然往上100个版本写100个 `^` 比较容易数不过来, 所以写成 `HEAD~100`.

现在, 我们要把当前版本回退到上一个版本 `add distributed`, 就可以使用 `git reset` 命令:

```git
$ git reset --hard HEAD^
HEAD is now at 2937c15 add distributed
```

`--hard` 参数的意义以后再说, 这里先使用. 

查看 `readme.txt` 的内容是不是版本 `add distributed`:

```git
$ cat readme.txt
Git is a distributed version control system.
Git is free software.
```

还可以继续回退到上一个版本 `wrote a readme file`, 不过, 先用 `git log` 看看现在版本库的状态:

```git
$ git log
commit 2937c152b91a09c5a723fce2d88d5a86d3f584ce (HEAD -> master)
Author: Tsui <kristophertsui@163.com>
Date:   Sat Dec 7 20:17:10 2019 +0800

    add distributed

commit bbd5bcef700db0f55d1f8c77b9a13fad6dc38abc
Author: Tsui <kristophertsui@163.com>
Date:   Sat Dec 7 20:09:08 2019 +0800

    wrote a readme file
```

最新的那个版本 `append GPL` 已经看不到了！好比你从21世纪坐时光穿梭机来到了19世纪, 想再回去已经回不去了, 怎么办?

办法其实还是有的, 只要上面的命令行窗口还没有被关掉, 你就可以顺着往上找啊找啊, 找到那个 `append GPL` 的 `commit id` 是 `d95c9ac...`, 于是就可以指定回到未来的某个版本:

```git
$ git reset --hard d95c9
HEAD is not at d95c9ac append GPL
```

版本号没必要写全, 前几位就可以了, Git 会自动去找. 当然也不能只写前一两位, 因为 Git 可能会找到多个版本号, 就无法确定是哪一个了.

再次查看 `readme.txt` 的内容:

```git
$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
```

Git 的版本回退速度非常快, 因为 Git 在内部有个指向当前版本的 `HEAD` 指针, 当你回退版本的时候, Git 仅仅是把 HEAD 从指向 `append GPL` 改为指向 `add distributed`. 然后顺便把工作区的文件更新了. 所以, 你让 `HEAD` 指向那个版本号, 你就把当前版本定位在哪.

现在, 退回到了某个版本, 关掉了电脑, 第二天又反悔了, 想恢复到新版本怎么办？找不到新版本的 `commit id` 怎么办?

在 Git 中, 总是有后悔药可以吃的. 当你用 `$ git reset --hard HEAD^` 回退到 `add distributed` 版本时, 再想恢复到 `append GPL`, 就必须找到 `append GPL` 的 commit id. Git 提供了一个命令 `git reflog` 用来记录你的每一次命令:

```git
$ git reflog
d95c9ac (HEAD -> master) HEAD@{0}: reset: moving to d95c9
2937c15 HEAD@{1}: reset: moving to HEAD^
d95c9ac (HEAD -> master) HEAD@{2}: commit: append GPL
2937c15 HEAD@{3}: commit: add distributed
bbd5bce HEAD@{4}: commit (initial): wrote a readme file
```

从输出可知, `append GPL` 的 commit id 是 `d95c9ac`, 现在, 你又可以乘坐时光机回到未来了.

## 工作区和暂存区

Git 和其他版本控制系统如 SVN 的一个不同之处就是有暂存区的概念.

* 工作区(Working Directory)

就是你在电脑里能看到的目录, 比如 `learngit` 文件夹就是一个工作区:

![alt 工作区](https://static.liaoxuefeng.com/files/attachments/919021113952544/0)

* 版本库(Repository)

工作区有一个隐藏目录 `.git`, 这个不算工作区, 而是 Git 的版本库.

Git 的版本库里存了很多东西, 其中最重要的就是称为 stage（或者叫 index）的暂存区, 还有 Git 为我们自动创建的第一个分支 `master`, 以及指向 `master` 的一个指针叫 `HEAD`.

![alt 版本库](https://static.liaoxuefeng.com/files/attachments/919020037470528/0)

前面我们说过把文件往 Git 版本库里添加的时候, 是分两步执行的:

第一步是用 `git add` 把文件添加进去, 实际上就是把文件修改添加到暂存区;

第二步是用 `git commit` 提交更改, 实际上就是把暂存区的所有内容提交到当前分支.

因为我们创建 Git 版本库时, Git 自动为我们创建了唯一一个 `master` 分支, 所以现在, `git commit` 就是往 `master` 分支上提交更改.

可以简单理解为, 需要提交的文件修改通通放到暂存区, 然后, 一次性提交暂存区的所有修改.

现在, 先对 `readme.txt` 做个修改, 比如加上一行内容:


```
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
```

然后, 在工作区新增一个 `LICENSE` 文本文件(内容随便写).

先用 `git status` 查看以下状态:

```git
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   readme.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        LICENSE

no changes added to commit (use "git add" and/or "git commit -a")
```

Git 非常清楚地告诉我们, `readme.txt` 被修改了, 而 `LICENSE` 还从来没有被添加过, 所以它的状态是 `Untracked`.

现在, 使用两次命令 `git add`, 把 `readme.txt` 和 `LICENSE` 都添加后, 用 `git status` 再查看一下:

```git
$ git status
On branch master
changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   LICENSE
        modified:   readme.txt

```

现在, 暂存区地状态就变成这样了:

![alt 暂存区](https://static.liaoxuefeng.com/files/attachments/919020074026336/0)

所以, `git add` 命令实际上就是把要提交的是所有修改放到暂存区(Stage), 然后, 执行 `git commit` 就可以一次性把暂存区的所有修改提交到分支.

```git
$ git commit -m "understand how stage works"
[master e500136] understand how stage works
 2 files changed, 2 insertions(+)
 create mode 100644 LICENSE
```

一旦提交后, 如果你又没对工作区做任何修改, 那么工作区就是"干净"的:

```git
$ git status
On branch master
nothing to commit, working tree clean
```

现在版本库变成了这样, 暂存区就没有任何内容了:

![alt 版本库](https://static.liaoxuefeng.com/files/attachments/919020100829536/0)

## 管理修改

现在, 假定你已经完全掌握了暂存区的概念. 下面, 我们要讨论的是, 为什么 Git 比其他版本控制系统设计得优秀, 因为 Git 跟踪并管理的是修改, 而非文件.

什么是修改？比如你新增了一行, 这就是一个修改；删除了一行, 也是一个修改；更改了某些字符, 也是一个修改；删了一些又加了一些, 也是一个修改；甚至创建了一个新文件, 也算是修改.

为什么说 Git 管理的是修改, 而不是文件呢？我们来做一个实验. 第一步, 对 readme.txt 做一个修改, 比如增加一行内容

```
$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes.
```

然后, 添加:

```git
$ git add readme.txt
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   readme.txt

```

然后, 再修改 readme.txt:

```
$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
```

提交:

```git
$ git commit -m "git tracks changes"
[master dd6783f] git tracks changes
 1 file changed, 1 insertion(+)
```

提交后, 再查看状态:

```git
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)

    modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

怎么第二次的修改没有被提交?

我们回顾一下操作过程:

第一次修改 --> `git add` --> 第二次修改 --> `git commit`

前面说过, Git 管理的是修改, 当你用 `git add` 命令后, 在工作区的第一次修改被放入暂存区, 准备提交, 但是, 在工作区的第二次修改并没有放入暂存区, 所以, `git commit` 只负责把暂存区的修改提交了, 也就是第一次的修改提交了, 第二次的修改不会被提交.

提交后, 用 `git diff HEAD -- readme.txt` 命令可以查看工作区和版本库里面最新版本的区别:

```git
$ git diff HEAD -- readme.txt
diff --git a/readme.txt b/readme.txt
index 76d770f..a9c5755 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,4 +1,4 @@
 Git is a distributed version control system.
 Git is free software distributed under the GPL.
 Git has a mutable index called stage.
-Git tracks changes.
+Git tracks changes of files.
```

可见, 第二次修改确实没有被提交.

那怎么提交第二次修改呢？你可以继续 `git add` 再 `git commit`, 也可以别着急提交第一次修改, 先 `git add` 第二次修改, 再 `git commit`, 就相当于把两次修改合并后一块提交了:

第一次修改 --> `git add` --> 第二次修改 --> `git add` --> `git commit`

## 撤销修改

你在 `readme.txt` 中添加了一行:

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
My stupid boss still prefers SVN.
```
在你准备提交的时侯, 你猛然发现了 `stupid boss` 可能会让你丢掉这个月的奖金.

既然错误发现得很及时, 就可以很容易地纠正它. 你可以删掉最后一行, 手动把文件恢复到上一个版本的状态. 如果用 `git status` 查看一下:

```git
$ git branch master
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

你可以发现, Git 会告诉你, `git restore` 可以丢弃工作区的修改:

```git
$ git restore readme.txt
```

命令 `git restore readme.txt` 意思就是, 把 `readme.txt` 文件在工作区的修改全部撤销, 这里有两种情况:

一种是 `readme.txt` 自修改后还没有被放到暂存区, 现在, 撤销修改就回到和版本库一模一样的状态;

一种是 `readme.txt` 已经添加到暂存区后, 又作了修改, 现在, 撤销修改就回到添加到暂存区后的状态.

总之, 就是让这个文件回到最近一次 `git commit` 或 `git add` 时的状态.

现在, 查看 `readme.txt` 的文件内容:

```
$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes.
```

文件内容果然复原了.

另外, `git checkout -- <file>` 也可以丢弃工作区的修改.

注意, `git checkout -- <file>` 命令中的 `--` 很重要, 没有 `--`, 就变成了“ 切换到另一个分支” 的命令, 会在后面的分支管理中用到.

******

如果你不但写了一些胡话, 还 `git add` 到暂存区了:

```git
$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes.
My stupid boss still prefers SVN.
$ git add readme.txt
```

庆幸的是, 你在 `commit` 之前发现了这个问题. 用 `git status` 查看一下, 修改只是添加到了暂存区, 还没有提交:

```git
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   readme.txt

```

Git 告诉我们, 用命令 `git restore --staged <file>` 可以把暂存区的修改撤销掉(unstage), 重新放回工作区:

```
$ git restore --staged readme.txt
```

再用 `git status` 查看一下, 现在暂存区是干净的, 工作区有修改:

```git
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   readme.txt

```

还记得如何丢弃工作区的修改吗?

```git
$ git checkout -- readme.txt
$ git status
On branch master
nothing to commit, working tree clean
```

同样, 把暂存区的修改撤销掉还可以使用命令 `git reset HEAD <file>`

```git
$ git reset HEAD readme.txt
Unstaged changes after reset:
M   readme.txt
```

`git reset` 命令既可以回退版本, 也可以把暂存区的修改回退到工作区. 当我们用 `HEAD` 时, 表示最新的版本.

现在, 假设你不但 改错了东西, 还从暂存区提交到了版本库, 怎么办呢？还记得[版本回退](#版本回退)一节吗？可以回退到上一个版本. 不过, 这是有条件的, 就是你还没有把自己的本地版本库推动到远程.

## 删除文件

在 Git 中, 删除也是一个修改操作. 先添加一个新文件 `test.txt` 到 Git 并且提交:

```git
$ git add test.txt
$ git commit -m "add test.txt"
[master 8c1b029] add test.txt
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
```

一般情况下, 通常直接在文件管理器中把没用的文件删了, 或者用 `rm` 命令删了:

```
$ rm test.txt
```

这个时候, Git 知道你删除了文件, 因此, 工作区和版本库就不一致了, `git status` 命令会立刻告诉你哪些文件被删除了:

```git
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

现在, 你有两个选择, 一是确实要从版本库中删除该文件那就用命令 `git rm` 删掉, 并且 `git commit`:

```git 
$ git rm test.txt
rm 'test.txt'
$ git commit -m "remove test.txt"
[master 1208428] remove test.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt
```

现在文件就从版本库中删除了.

另一种情况就是删错了, 因为版本库里还有呢, 所以可以很轻松地把误删的文件恢复到最新版本:

```git
$ git restore test.txt
```

也可以使用如下命令:

```git
$ git checkout -- test.txt
```

`git checkout` 其实是用版本库里的版本替换工作区地版本无论工作区是修改还是删除, 都可以一键还原.

> **注意:** 从来没有被添加到版本库就被删除的文件, 是无法恢复的!

# 远程仓库
## 创建SSH Key

在用户主目录下, 看看有没有 `.ssh` 目录, 如果有, 再看看这个目录下有没有 `id_rsa` 和 `id_rsa.pub` 这两个文件. 如果没有, 创建 SSH Key:

```git
$ ssh-keygen -t rsa -C "ouremail@example.com"
```

`id_rsa` 和 `id_rsa.pub` 这两个文件就是 SSH Key 的密钥对, `id_rsa` 是私钥, 不能泄露除去, `id_rsa.pub` 是公钥, 可以放心地告诉任何人. 

然后登陆 GitHub 添加 SSH Key.

为什么 GitHub 需要 SSH Key 呢？因为 GitHub 需要识别出你推送的提交确实是你推送的, 而不是别人冒充的, 而 Git 支持 SSH 协议, 所以, GitHub 只要知道了你的公钥, 就可以确认只有你自己才能推送.

当然, GitHub 允许你添加多个 Key. 假定你有若干电脑, 你一会儿在公司提交, 一会儿在家里提交, 只要把每台电脑的 Key 都添加到 GitHub, 就可以在每台电脑上往 GitHub 推送了.

最后友情提示, 在 GitHub 上免费托管的 Git 仓库, 任何人都可以看到喔（但只有你自己才能改）. 所以, 不要把敏感信息放进去.

## 添加远程库

在本地的仓库下运行命令:

```git 
$ git remote add origin git@github.com:TsuiGit/learngit.git
```

添加后, 远程库的名字就是 'origin', 这是 Git 默认的叫法, 也可以改成别的, 但是 `origin` 这个名字一看就知道是远程库.

下一步就可以把本地库的所有内容推送到远程库上:

```git
$ git push -u origin master
Counting objects: 100% (20/20), done.
Delta compression using up to 4 threads
Compressing objects: 100% (16/16), done.
Writing objects: 100% (20/20), 1.67 KiB | 428.00 KiB/s, done.
Total 20 (delta 5), reused 0 (delta 0)
remote: Resolving deltas: 100% (5/5), done.
To github.com:TsuiGit/learngit.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'
```

把本地库的内容推送到远程, 用 `git push` 命令, 实际上是吧当前分支 `master` 推送到远程.

由于远程库是空的, 我们第一次推送 `master` 分支时, 加上了 `-u` 参数, Git 不但会把本地的 `master` 分支内容推送到远程新的 `master` 分支, 还会把本地的 `master` 分支和远程的 `master` 分支关联起来, 在以后的推送或者拉取时就可以简化命令.

推送成功后, 可以立刻在 GitHub 页面中看到远程库的内容已经和本地一模一样:

![alt GitHub](https://s2.ax1x.com/2019/12/21/QvtjZ6.png)

从现在起, 只要本地做了修改, 就可以通过命令:

```git
$ git push origin master
```

把本地 `master` 分支的最新修改推送至 GitHub, 现在, 你就拥有了真正的分布式版本库.

## SSH 警告

当你第一次使用 Git 的 `clone` 或者 `push` 命令连接 GitHub 时, 会得到一个警告:

```
The authenticity of host 'github.com (13.229.188.59)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

这是因为 Git 使用 SSH 连接, 而 SSH 连接在第一次验证 GitHub 服务器的 Key 时, 需要你确认 GitHub 的 Key 的指纹信息是否真的来自 GitHub 的服务器, 输入 `yes` 回车即可.

Git 会输出一个警告, 告诉你已经把 GitHub 的 Key 添加到 本机的一个信任列表里了:

```
Warning: Permanently added 'github.com,13.229.188.59' (RSA) to the list of known hosts.
```

这个警告只会出现一次, 后面的操作就不会有任何警告了.

如果你是在担心有人冒充 GitHub 服务器, 输入 `yes` 前可以对照 GitHub 的 RSA Key 的指纹信息是否与 SSH 连接给出的一致.

## 从远程库克隆

现在, 假设我们从零开发, 那么最好的方式是先创建远程库, 然后, 从远程库克隆.

首先, 登录 GitHub, 创建一个新的仓库, 名字叫 `gitskills`:

![alt CreatPropersity](https://s2.ax1x.com/2019/12/21/QvdMSe.png)

我们勾选 `Initialize this repository with a README`, 这样 GitHub 会自动为我们创建一个 `README.md` 文件. 创建完毕后, 可以看到 `README.md` 文件:

![alt README](https://s2.ax1x.com/2019/12/21/Qvdfl4.png)

现在, 远程库已经准备好了, 下一步是用 `git clone` 克隆一个本地库:

```git
$ git clone git@github.com:TsuiGit/gitskills.git
Cloning into 'gitskills'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```

然后进入 `gitskills` 目录查看, 已经有 `README.md` 文件了:

```
$ cd gitskills
$ ls
README.md
```

如果有多个人协作开发, 那么每个人各自从远程克隆一份就可以了.

注意到 GitHub 给出的地址不止一个, 还可以用 `https://github.com/TsuiGit/gitskills.git` 这样的地址. 实际上, Git 支持多种协议, 默认的 `git://` 是用 SSH, 但也可以使用 `https` 等其他协议.

使用 `https` 除了速度慢以外, 最大的麻烦是每次推送都必须输入口令, 但是在某些只开放 http 端口的公司内部就无法使用 `SSH` 协议而只能用 `https`.

# 分支管理

分支在实际中有什么用呢？假设你准备开发一个新功能, 但是需要两周才能完成, 第一周你写了 50% 的代码, 如果立刻提交, 由于代码还没写完, 不完整的代码库会导致别人不能干活了. 如果等代码全部写完再一次提交, 又存在丢失每天进度的巨大风险.

现在有了分支, 就不用怕了. 你创建了一个属于你自己的分支, 别人看不到, 还继续在原来的分支上正常工作, 而你在自己的分支上干活, 想提交就提交, 直到开发完毕后, 再一次性合并到原来的分支上, 这样, 既安全, 又不影响别人工作.

其他版本控制系统如 SVN 等都有分支管理, 但是用过之后你会发现, 这些版本控制系统创建和切换分支比蜗牛还慢, 简直让人无法忍受, 结果分支功能成了摆设, 大家都不去用.

但 Git 的分支是与众不同的, 无论创建、切换和删除分支, Git 在 1 秒钟之内就能完成！无论你的版本库是 1 个文件还是 1 万个文件.

### 创建与合并分支

在[版本回退](#版本回退)里, 你已经知道, 每次提交, Git 都把它们串成一条时间线, 这条时间线就是一个分支. 截止到目前, 只有一条时间线, 在 Git 里, 这个分支叫**主分支**, 即 `master` 分支. `HEAD` 严格来说不是指向提交, 而是指向 `master`, `master` 才是指向提交的, 所以, `HEAD` 指向的就是当前分支.

一开始的时候, `master` 分支是一条线, Git 用 `master` 指向最新的提交, 再用 `HEAD` 指向 `master`, 就能确定当前分支, 以及当前分支的提交点:

![alt master分支](https://static.liaoxuefeng.com/files/attachments/919022325462368/0)

每次提交, `master` 分支都会向前移动一步, 这样, 随着你不断提交, `master` 分支的线也越来越长.

当我们创建新的分支, 例如 `dev` 时, Git 新建了一个指针叫 `dev`, 指向 `master` 相同的提交, 再把 `HEAD` 指向 `dev`, 就表示当前分支在 `dev` 上:

![alt dev分支](https://static.liaoxuefeng.com/files/attachments/919022363210080/l)

Git 创建一个分支很快, 因为除了增加一个 `dev` 指针, 改改	`HEAD` 的指向, 工作区的文件都没有任何变化!

不过, 从现在开始, 对工作区的修改和提交就是针对 `dev` 分支了, 比如新提交一次后, `dev` 指针往前移动一步, 而 `master` 指针不变:

![alt](https://static.liaoxuefeng.com/files/attachments/919022387118368/l)

假如我们在 `dev` 上的工作完成了, 就可以把 `dev` 合并到 `master` 上. Git 怎么合并呢？最简单的方法, 就是直接把 `master` 指向 `dev` 的当前提交, 就完成了合并:

![alt 合并分支](https://static.liaoxuefeng.com/files/attachments/919022412005504/0)

所以 Git 合并分支也很快！就改改指针, 工作区内容也不变!

合并完分支后, 甚至可以删除 `dev` 分支. 删除 `dev` 分支就是把 `dev` 指针给删掉, 删掉后, 我们就剩下了一条 `master` 分支:

![alt 删除分支](https://static.liaoxuefeng.com/files/attachments/919022479428512/0)

下面开始实战. 

首先, 我们创建 `dev` 分支, 然后切换到 `dev` 分支:

```git
$ git checkout -b dev
Switched to a new branch 'dev'
```

`git checkout` 命令加上 `-b` 参数表示创建并切换, 相当于以下两条命令:

```git
$ git branch dev
$ git checkout dev
Switched to branch 'dev'
```

然后, 用 `git branch` 命令查看当前分支:

```git
$ git branch
* dev
  master
```

`git branch` 命令会列出所有分支, 当前分支前面会标一个 `*` 号.

然后, 我们就可以在 `dev` 分支上正常提交, 比如对 `readme.txt` 做个修改, 加上一行:

```
Creating a new branch is quick.
```

然后提交:

```git
$ git add readme.txt
$ git commit -m "branch test"
[dev fc04d69] branch test
 1 file changed, 1 insertion(+)
```

现在, `dev` 分支的工作完成, 我们就可以切换回 `master` 分支:

```git
$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
```

切换回 `master` 分支后, 再查看一个 `readme.txt` 文件, 刚才添加的内容不见了！因为那个提交是在 `dev` 分支上, 而 `master` 分支此时的提交点并没有变:

![alt](https://static.liaoxuefeng.com/files/attachments/919022533080576/0)

现在, 我们把 `dev` 分支的工作成果合并到 `master` 分支上:

```git
$ git merge dev
Updating 1208428..fc04d69
Fast-forward
 readme.txt | 1 +
  1 file changed, 1 insertion(+)
```

`git merge` 命令用于合并指定分支到当前分支. 合并后, 再查看 `readme.txt` 的内容, 就可以看到, 和 `dev` 分支的最新提交是完全一样的.

注意到上面的 `Fast-forward` 信息, Git 告诉我们, 这次合并是"快进模式", 也就是直接把 `master` 指向 `dev` 的当前提交, 所以合并速度非常快.

当然, 也不是每次合并都能 `Fast-forward`.

合并完成后, 就可以放心地删除 `dev` 分支了:

```git
$ git branch -d dev
Deleted branch dev (was fc04d69).
```

删除后, 查看 `branch`, 就只剩下 `master` 分支了:

```git
$ git branch
* master
```

因为创建、合并和删除分支非常快, 所以 Git 鼓励你使用分支完成某个任务, 合并后再删掉分支, 这和直接在 `master` 分支上工作效果是一样的, 但过程更安全.

注意到切换分支使用 `git checkout <branch>`, 而前面讲过的撤销修改则是 `git checkout -- <file>`, 同一个命令, 有两种作用, 确实有点令人迷惑.

实际上, 切换分支这个动作, 用 `switch` 更科学. 因此, 最新版本的 Git 提供了新的 `git switch` 命令来切换分支:

创建并切换到新的 `dev` 分支, 可以使用:

```git
$ git switch -c dev
```

直接切换到已有的 `master` 分支, 可以使用:

```git
$ git switch master
```

使用新的 `git switch` 命令, 比 `git checkout` 要更容易理解.

## 空分支的创建

如果想要创建一个新的分支, 可以使用 `git checkout -b newbranch` 命令, 然后使用 `git checkout branchname` 命令可以在分支间切换.

但是这样创建的分支非空. 如果想要创建一个空分支, 则需要使用 `git checkout -orphan emptybranch` 命令[^emptybranch]. 该命令创建的分支不承接之前所有的提交, 此时使用 `git rm -rf .` 命令清除内容, 就得到了一个空分支. 空分支在不提交任何内容的情况下, `git branch` 命令是不显示该分支的. 可以添加一个 `README.md` 文件描述提交, 这样就可以看见新分支了.
[^emptybranch]: Geometryolife.[如何快速在 Git 中创建一个空分支（孤立分支）](https://zhuanlan.zhihu.com/p/453126177)[OL].(2022-1-4)[2023-5-19].

## 分支重命名
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

## 解决冲突

准备新的 `feature1` 分支, 继续我们的新分支开发:

```git
$ git switch -c feature1
Switched to a new branch 'feature1`
```

修改 `readme.txt` 最后一行, 改为:

```
Creating a new branch is quick AND simple.
```

在 `feature1` 分支提交:

```git
$ git add readme.txt
$ git commit -m "AND simple"
[feature1 1d8d670] AND simple
 1 file changed, 1 insertion(+), 1 deletion(-)
```

切换到 `master` 分支:

```git
$ git switch master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
```

Git 还会自动提示我们当前 `master` 分支比远程的 `master` 分支要超前一个提交.

在 `master` 分支上把 `readme.txt` 文件的最后一行改为:

```
Creating a new branch is quick & simple.
```

提交:

```git
$ git add readme.txt
$ git commit -m "& simple"
[master e3158c4] & simple
 1 file changed, 1 insertion(+), 1 deletion(-)
```

现在, `master` 分支和 `feature1` 分支各自都分别有新的提交, 变成了这样:

![alt 多分支提交](https://static.liaoxuefeng.com/files/attachments/919023000423040/0)

这种情况下, Git 无法执行"快速合并", 只能试图把各自的修改合并起来, 但这种合并就有可能会冲突, 我们试试看:

```git
$ git merge feature1
Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
Automatic merge failed; fix conflicts and then commit the result.
```

果然冲突了！Git 告诉我们, `readme.txt` 文件存在冲突, 必须手动解决冲突后在进行提交. `git status` 也可以告诉我们冲突的文件:

```git
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

我们可以直接查看 readme.txt 的内容:

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes.
Creating a new branch is quick AND simple.
```

Git 用 `<<<<<<<`, `=======`, `>>>>>>>` 标记出不同分支的内容, 我们修改如下后保存:

```
Creating a new branch is quick and simple.
```

再提交:

```git
$ git add readme.txt
$ git commit -m "conflict fixed"
[master c3d1fe5] conflict fixed
```

现在, `master` 分支和 `feature1` 分支变成了下图所示:

![alt 多分枝](https://static.liaoxuefeng.com/files/attachments/919023031831104/0)

再用带参数的 `git log` 也可以看到分支的合并情况:

```git
$ git log --graph --pretty=oneline --abbrev-commit
*   c3d1fe5 (HEAD -> master) conflict fixed
|\
| * 1d8d670 (feature1) AND simple
* | e3158c4 & simple
|/
* fc04d69 branch test
* 1208428 (origin/master) remove test.txt
* 8c1b029 add test.txt
* dd6783f git tracks changes
* e500136 understand how stage works
* d95c9ac add distributed under GPL
* 2937c15 add distributed
* bbd5bce wrote a readme file
```

最后, 删除 `feature` 分支:

```git
$ git branch -d feature1
Deleted branch feature1 (was 1d8d670).
```

工作完成.

## 分支管理策略

通常, 合并分支时, 如果可能, Git 会用 `Fast forward` 模式, 但这种模式下, 删除分支后, 会丢掉分支信息.

如果要强制禁用 `Fast forward` 模式, Git 就会在 merge 时生成一个新的 commit, 这样, 从分支历史上就可以看出分支信息.

下面实战一下 `--no-ff` 方式的 `git merge`:

首先, 仍然创建并切换 `dev` 分支:

```git
$ git switch -c dev
Switched to a new branch 'dev'
```

修改 readme.txt 文件, 并提交一个新的 commit:

```git
$ git add readme.txt
$ git commit -m "add merge"
[dev b5cb3a5] add merge
 1 file changed, 1 insertion(+)
```

现在, 我们切换回 `master`:

```git
$ git switch master
Switched to branch 'master'
```

准本合并 `dev` 分支, 请注意 `--no-ff` 参数, 表示禁用 `Fast forward`:

```git
$ git merge --no-ff -m "merge with no-ff" dev
Merge made by the 'recursive' strategy.
 readme.txt | 1 +
 1 file changed, 1 insertion(+)
```

因为本次合并需要创建一个新的 commit, 所以加上 `-m` 参数, 把 commit 描述写进去.

合并后, 我们用 `git log` 查看分支历史:

```git
$ git log --graph --pretty-oneline --abbrev-commit
*   48c2cfe (HEAD -> master) merge with no-ff
|\
| * b5cb3a5 (dev) add merge
|/
*   c3d1fe5 conflict fixed
|\
| * 1d8d670 AND simple
* | e3158c4 & simple
|/
* fc04d69 branch test
* 1208428 (origin/master) remove test.txt
* 8c1b029 add test.txt
* dd6783f git tracks changes
* e500136 understand how stage works
* d95c9ac add distributed under GPL
* 2937c15 add distributed
* bbd5bce wrote a readme file
```

可以看到, 不使用 `Fast forward` 模式, merge 后就像这样:

![alt NoFastforward](https://static.liaoxuefeng.com/files/attachments/919023225142304/0)

### 分支策略

在实际开发中, 我们应该按照几个基本原则进行分支管理:

首先, `master` 分支应该是非常稳定的, 也就是仅用来发布新版本, 平时不能在上面该或;

拿在哪干活呢？干活都在 `dev` 分支上, 也就是说, `dev` 分支是不稳定的, 到某个时候, 比如 1.0 版本发布时, 再把 `dev` 分支合并到 `master` 上, 在 `master` 分支发布 1.0 版本;

你和你的小伙伴们每个人都在 `dev` 分支上干活, 每个人都有自己的分支, 时不时地往 `dev` 分支上合并就可以了.

所以, 团队合作的分支看起来就像这样:

![alt TeamCooperation](https://static.liaoxuefeng.com/files/attachments/919023260793600/0)

## Bug 分支

## Feature 分支

## 多人协作

## Rebase

# 标签管理

发布一个版本时, 我们通常先在版本库中打一个标签(tag), 这样, 就唯一确定了打标签时刻的版本. 将来无论什么时候, 取某个标签的版本, 就是把那个打标签的时刻的历史版本取出来. 所以, 标签也是版本库的一个快照.

Git 的标签虽然是版本库的快照, 但其实它就是指向某个 commit 的指针(跟分支很像对不对？但是分支可以移动, 标签不能移动), 所以, 创建和删除标签都是瞬间完成的.

Git 有 commit, 为什么还要引入 tag?

"请把上周一的那个版本打包发布, commit 号是 6a5819e..."

一串乱七八糟的数字不好找!

如果换一个办法:

"请把上周一的那个版本打包发布, 版本号是 v1.2"

"好的, 按照 tag v1.2 查找 commit 就行!"

所以, tag 就是一个让人容易记住的有意义的名字, 它跟某个 commit 绑在一起.

## 创建标签

在 Git 中打标签非常简单, 首先, 切换到需要打标签的分支上:

```git
$ git branch
* dev
  master
$ git checkout master
Switched to branch ''master'
```

然后敲命令 `git tag <name>` 就可以打一个新标签:

```git
$ git tag v1.0
```

可以用命令 `git tag` 查看所有标签:

```git
$ git tag
v1.0
```

默认标签是打在最新提交的 commit 上的. 有时候, 如果忘了打标签, 比如, 现在已经是周五了, 但应该在周一打的标签没有打, 怎么办?

方法是找到历史提交的 commit id, 然后打上就可以了:

```git
$ git log --pretty=oneline --abbrev-commit
48c2cfe (HEAD -> master, tag: v1.0) merge with no-ff
b5cb3a5 (dev) add merge
c3d1fe5 conflict fixed
e3158c4 & simple
1d8d670 AND simple
fc04d69 branch test
1208428 (origin/master) remove test.txt
8c1b029 add test.txt
dd6783f git tracks changes
e500136 understand how stage works
d95c9ac add distributed under GPL
2937c15 add distributed
bbd5bce wrote a readme file
```

比方说要对 `conflict fixed` 这次提交打标签, 它对应的 commit id 是 `c3d1fe5`, 敲入命令:

```git
$ git tag v0.9 c3d1fe5
```

再用命令 `git tag` 查看标签:

```git
$ git tag
v0.9
v1.0
```

注意, 标签不是按时间顺序列出, 而是按字母排序的. 可以用 `git show <tagname>` 查看标签信息:

```git
$ git show v0.9
commit c3d1fe529ae0e5fcb98064e7836515ba49f7eb7f (tag: v0.9)
Merge: e3158c4 1d8d670
Author: Tsui <kristophertsui@163.com>
Date:   Sat Jan 11 15:49:06 2020 +0800

    conflict fixed

diff --cc readme.txt
...(省略)
```

可以看到, `v0.9` 确实打在 `add merge` 这次提交上.

还可以创建带有说明的标签, 用 `-a` 指定标签名, `-m` 指定说明文字:

```git
$ git tag -a v0.1 -m "version 0.1 realeased" d95c9ac
```

用命令 `git show <tagname>` 可以看到说明文字:

```git
$ git show v0.1
tag v0.1
Tagger: Tsui <kristophertsui@163.com>
Date:   Sat Jan 11 17:37:24 2020 +0800

version 0.1 released

commit d95c9ac1905470961c5ad29b445afff648971661 (tag: v0.1)
Author: Tsui <kristophertsui@163.com>
Date:   Sat Dec 7 20:23:19 2019 +0800

    add distributed under GPL

diff --git a/readme.txt b/readme.txt
```

> **注意:** 标签总是和某个 commit 挂钩. 如果这个 commit 既出现在 master 分支, 又出现在 dev 分支, 那么在这两个分支上都可以看到这个标签.

## 操作标签

如果标签打错了, 也可以删除:

```git
$ git tag -d v0.1
Deleted tag 'v0.1' (was 20646c1)
```

因为创建的标签都只存储在本地, 不会自动推送到远程. 所以, 打错的标签可以在本地安全删除.

如果要推送到某个标签到远程, 使用命令 `git push origin <tagname>`:

```git
$ git push origin v1.0
Total 16 (delta 6), reused 0 (delta 0)
remote: Resolving deltas: 100% (6/6), done.
To github.com:TsuiGit/learngit.git
 * [new tag]         v1.0 -> v1.0
```

或者, 一次性推送全部尚未推送到远程的本地标签:

```git
$ git push origin --tags
Total 0 (delta 0), reused 0 (delta 0)
To github.com:TsuiGit/learngit.git
 * [new tag]         v0.9 -> v0.9
```

如果标签已经推送到远程, 要删除标签就麻烦一点, 先从本地删除:

```git
$ git tag -d v0.9
Deleted tag 'v0.9' (was c3d1fe5)
```

然后, 从远程删除. 删除命令也是 push, 但是格式如下:

```git
$ git push origin :refs/tags/v0.9
To github.com:TsuiGit/learngit.git
 - [deleted]         v0.9
```

要看看是否真的从远程库删除了标签, 可以登陆 GitHub 查看.

## 使用 GitHub

我们一直用 GitHub 作为免费的远程仓库, 如果是个人的开源项目, 放到 GitHub 上是完全没有问题的. 其实 GitHub 还是一个开源协作社区, 通过 GitHub, 既可以让别人参与你的开源项目, 也可以参与别人的开源项目.

在 GitHub 出现以前, 开源项目开源容易, 但让广大人民群众参与进来比较困难, 因为要参与, 就要提交代码, 而给每个想提交代码的群众都开一个账号那是不现实的, 因此, 群众也仅限于报个 bug, 即使能改掉 bug, 也只能把 diff 文件用邮件发过去, 很不方便.

但是在 GitHub 上, 利用 Git 极其强大的克隆和分支功能, 广大人民群众真正可以第一次自由参与各种开源项目了.

如何参与一个开源项目呢？比如人气极高的 bootstrap 项目, 这是一个非常强大的 CSS 框架, 你可以访问它的项目主页 https://github.com/twbs/bootstrap, 点 Fork 就在自己的账号下克隆了一个 bootstrap 仓库, 然后, 从自己的账号下 clone:

```git
$ git clone git@github.com:TsuiGit/bootstrap.git
```

一定要从自己的账号下 clone 仓库, 这样你才能推送修改. 如果从 bootstrap 的作者的仓库地址 `git@github.com:twbs/bootstrap.git` 克隆, 因为没有权限, 你将不能推送修改.

Bootstrap 的官方仓库 `twbs/bootstrap`、你在 GitHub 上克隆的仓库 `my/bootstrap`, 以及你自己克隆到本地电脑的仓库, 他们的关系就像下图显示的那样:

![alt GitHub仓库关系图](https://s2.ax1x.com/2020/01/12/lofTBT.png)

如果你想修复 bootstrap 的一个 bug, 或者新增一个功能, 立刻就可以开始干活, 干完后, 往自己的仓库推送.

如果你希望 bootstrap 的官方库能接受你的修改, 你就可以在 GitHub 上发起一个 pull request. 当然, 对方是否接受你的 pull request 就不一定了.

### 克隆远程分支
#### 单分支的克隆

想要将远程仓库的一个分支克隆到本地, 只需要增加 `-b` 参数:

```git
git clone -b branchname git@gitee.com:username/repositoryname.git
```

#### 所有分支的克隆

使用 `git clone` 克隆远程仓库只包含主分支, 其他分支是不会被克隆到本地的.

如果想要把远程仓库的所有分支都克隆到本地, 首先需要在本地也建立相应的分支. 即

```git
git checkout -b branchname origin/branchname
```

这样就把远程仓库的 `branchname` 分支克隆到本地了. 参考 [怎么用git clone 远程的所有分支](https://www.jianshu.com/p/0fe715a7fbb3).

## 码云

## 自定义 Git

### 忽略特殊文件

### 配置别名

### 搭建 Git 服务器

## 使用 SourceTree

