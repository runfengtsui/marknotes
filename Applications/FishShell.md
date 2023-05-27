---
Title: Fish 终端的安装与使用
Author: 邱彼郑楠
Date: 2023-03-14
Modified: 2023-05-27
---

# 安装

最简单的安装方法是使用包管理工具, 如 `apt`, 即使用 `apt install fish` 命令安装. 但这样安装得到的不是最新版本. 可以从 [Fish Shell 官网](https://fishshell.com/) 或者 [Github 主页](https://github.com/fish-shell/fish-shell.git) 查看最新的版本.

## Ubuntu

在 Ubuntu 系统, Fish Shell 维护团队给出了 [PPA description](https://launchpad.net/~fish-shell/+archive/ubuntu/release-3), 所以可以通过增加源的方式安装最新版本:

```bash
sudo apt-add-repository ppa:fish-shell/release-3
sudo apt update
sudo apt install fish
```

## 深度操作系统

在深度操作系统上, 选择采用源码编译的方式安装. 根据 [Dependencies](https://github.com/fish-shell/fish-shell#dependencies-1) 中的介绍, 需要以下工具

* Rust (version 1.67 or later)
* a C++11 compiler (g++ 4.8 or later, or clang 3.3 or later)
* CMake (version 3.5 or later)

> Rust 的安装见 [Rust入门笔记｜如何安装Rust-超全指南](https://zhuanlan.zhihu.com/p/618513180).

首先, 安装一些基础的包[^install]

```bash
sudo apt install build-essential ncurses-dev libncurses5-dev libpcre2-dev gettext
```

然后, 下载或者克隆源码

```bash
git clone git@github.com:fish-shell/fish-shell.git
```

在 `fish-shell` 文件夹下创建 `build` 文件夹用来存放 `cmake` 之后得到的文件, 避免和 `fish-shell` 文件夹下的文件混乱.

```bash
mkdir build; cd build
cmake ..
# 编译
make
# 安装
sudo make install
```

流程并不复杂, 最后 `fish`  安装到了 `/usr/local/bin` 文件夹下. 但在编译的过程中除了网络问题之外遇到了 `Unable to find libclang: "couldn't find any valid shared libraries matching: ['libclang.so', 'libclang-*.so', 'libclang.so.*', 'libclang-*.so.*']` 的问题. 大概是编译的时候使用的是 `clang` 而不是 `g++`, 最后通过安装 `clang` 得以解决.

```bash
sudo apt install clang
```

# 配置
## 默认Shell

使用 `chsh` 命令可以设置默认 Shell[^install]

```bash
chsh -s /usr/bin/fish
```

重启终端, 此时打开的就是 Fish Shell. 如果想要重新设置默认 Shell 为 Bash，使用相同的命令

```bash
chsh -s /usr/bin/bash
```

> 深度操作系统在默认终端使用 `chsh -s /usr/local/bin/fish` 是不起作用的. 这是因为打开终端后调用的是 `/usr/bin/fish`, 而安装的路径是 `/usr/local/bin/fish`, 所以可以通过设置软链接 `sudo ln -s /usr/local/bin/fish /usr/bin/fish` 来解决这个问题. 注意此时终端设置中 Shell 配置为 `$SHELL`.

## Oh-My-Fish

`Oh-My-Fish` 是一个可以美化 Fish Shell 的一个工具, 根据 [安装指导](https://github.com/oh-my-fish/oh-my-fish#installation), 将 `oh-my-fish` 仓库克隆到本地, 使用 `/bin/install` 工具进行安装.

```bash
git clone git@github.com:oh-my-fish/oh-my-fish.git
cd oh-my-fish
bin/install --offline
```

可以通过 `omf list` 命令查看是否安装成功. 安装并改变主题, 安装插件, 更新包等都可以通过 `omf` 来进行, 详细参考 [Oh My Fish! 让你的 Shell 漂亮起来](https://zhuanlan.zhihu.com/p/35448750) 这一篇文章.

## 配置文件

Fish Shell 的配置文件在 `~/.config/fish/config.fish`.

* 增加别名 `alias vim="nvim"`
* 添加环境变量 `set -x PATH path $PATH`

# 脚本编程
## 解释器路径

每一个脚本文件需要指定解释器, 即必须将 `#!/path/to/fish` 放在文件的头部.

## 自动获取路径

一般脚本想要在任何地方都能调用, 可以使用绝对路径. 还有一种方法就是使用 `dirname` 命令自动获取路径. 关于 `dirname` 的使用可以参考 [Shell 小技巧之dirname命令的使用](https://blog.csdn.net/evglow/article/details/106260462).

Bash 脚本往往和 `$0` 变量配合可以获取当前脚本所在的路径, 但是 Fish 中没有 `$0` 这个变量, 根据文档中 [special-variables](https://fishshell.com/docs/current/fish_for_bash_users.html#special-variables) 中的介绍, 变量 `status filename` 对应中 `$0` 变量. 所以对应于 Bash 中 `$(cd $(dirname $0); pwd)` 的 Fish 的用法是 `(cd (dirname (status filename)); pwd)`.

[^install]: 渔鳍.[用户友好的shell程序 —— Fish shell的安装和配置](https://zhuanlan.zhihu.com/p/488450129)[OL].(2022-3-27)[2023-5-26].

