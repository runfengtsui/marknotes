---
Title: 深度操作系统
Author: 邱彼郑楠
Date: 2023-05-24
Modified: 2023-05-25
---

# 编辑器
## Vim 

不打算使用 Vim 编辑器, 考虑将其完全卸载, 使用 `apt` 包管理工具进行卸载:

```bash
sudo apt remove vim
sudo apt remove vim-runtime
sudo apt remove vim-tiny
sudo apt remove vim-common
sudo apt remove vim-scripts
sudo apt remove vim-doc
```

> **注意**: 如果只运行了 `sudo apt remove vim`, `vim` 命令无法运行, 但是 `vi` 命令还是可以运行的. 所以一定要完全卸载掉.

## Neovim

深度操作系统可以在 [Releases](https://github.com/neovim/neovim/releases) 上下载 `nvim.appimage` 文件直接使用 Neovim. 详细介绍见 [Neovim 的安装](./Neovim.md#Deepin).

## 配置

Neovim 的配置在 Windows 的子系统 [WSL2](./WSL2.md#Editor) 中已经做过, 相关的知识见 [Neovim 教程](./Neovim.md#Tutorial), 具体的配置文件在 [NeovimConfiguration](https://gitee.com/runfengtsui/neovim-config).

现在不需要重新配置. 首先将原来的配置文件克隆过来:

```git
git clone git@gitee.com:runfengtsui/neovim-config.git ~/.config/nvim
```

然后安装 Packer 插件管理器,

```git
git clone --depth 1 https://github.com/wbthomason/packer.nvim\
 ~/.local/share/nvim/site/pack/packer/start/packer.nvim
```

安装成功后, 打开 Neovim, 命令模式下执行 `:PackerSync`, 安装所有插件. 插件安装完毕就配置完成了.

> **注意**. Pyright 等的安装以及 `markdown-preview.nvim` 插件需要使用 `npm` 工具, 见 [npm 的安装](./npm.md#安装). 否则 Neovim 会提示报错.

# 编程语言
## 北太天元

[北太天元](https://baltamatica.com/download.html) 提供了深度操作系统的软件包, 注册帐号之后直接下载即可.

对于下载好的安装包, 使用 `dpkg` 进行安装(北太天元的安装目前依赖于 `gnuplot`, 如果没有安装需要使用 `sudo apt install gnuplot` 进行安装.)

```bash
sudo dpkg -i baltamatica_2.1.1_deepin20_amd64.deb
```

安装完成后就可以使用 `baltamatica.sh` 命令启动北太天元软件.

如果想要在终端下打开北太天元, 执行的是 `baltamaticaC.sh` 文件, 这个文件位于 `/opt/Baltamatica/bin/` 文件夹下, 默认是不能在任意地方使用的. 此时有几种方法来解决这个问题

* 配置别名. 如使用别名 `baltam`, 使其指向 `/opt/Baltamatica/bin/baltamaticaC.sh`, 这是最简单的方式.
* 改写 `/usr/bin/baltamatica.sh` 文件. 能够在任意地方启动软件的原因是 `/usr/bin/` 这个文件夹有一个 `baltamatica.sh` 文件. 注意这个文件和 `/opt/Baltamatica/bin/` 目录下的 `baltamatica.sh` 不是一样的. 实际上, `/usr/bin/baltamatica.sh` 执行的是 `/opt/bin/baltamatica.sh`, 即 `/usr/bin/baltamatica.sh` 的内容如下:

```bash
#!/bin/sh
#filename baltamatica.sh
exec /opt/Baltamatica/bin/baltamatica.sh
```

所以只需要将上述文件中的 `baltamatica.sh`  替换为 `baltamaticaC.sh` 即可使用 `baltamatica.sh` 命令[^baltam] 在终端的任意地方打开北太天元.

```bash
sed -i "s@baltamatica.sh@baltamaticaC.sh@g" /usr/bin/baltamatica.sh
```

> **注意** 直接改写 `/usr/bin/baltamatica.sh` 文件会导致桌面上的北太天元失效, 因为其使用的命令是 `baltamatica.sh`, 现在 `baltamatica.sh` 指向了命令行版本, 自然启动不起来图形界面.

* 新建脚本文件. 类似于 `/usr/bin/baltamatica.sh` 文件中的内容, 新建一个脚本文件去执行 `/opt/Baltamatica/bin/baltamaticaC.sh`, 同时将这个文件放在 `$PATH` 变量中存在的路径下即可. 这也解决了直接改写图形界面无法启动的问题.

## Julia

从 [官网](https://julialang.org/downloads/) 下载 Generic Linux on x86 的 64-bit 最新版的包. 如果网络比较慢, 可以考虑使用 [清华大学开源镜像](https://mirrors.tuna.tsinghua.edu.cn/julia-releases/bin/) 下载对应版本.

下载完成后, 使用 `tar` 命令解压缩

```bash
tar xvzf julia-1.9.0-linux-x86_64.tar.gz
```

此时 `julia-1.9.0/bin/julia` 就可以直接运行 Julia. 为了在终端任意地方使用 Julia, 将文件夹 `julia-1.9.0` 全部移至 `/opt/` 目录下, 并建立软链接 `/usr/bin/julia` 指向 `/opt/julia-1.9.0/bin/julia`.

```bash
sudo mv julia-1.9.0 /opt/
sudo ln -s /opt/julia-1.9.0/bin/julia /usr/bin/julia
```

## Python

深度操作系统自带 Python 和 Python3, 其中 Python 是 2.7.16 版本, python3 是 3.7.3 版本.

> **注意** 不要尝试更新系统自带的 Python 和 Python3, 这样会使得系统崩溃. 如果想要使用其他版本的 Python3, 可以使用虚拟环境隔离[^python].

[^baltam]: woclass.[将 baltamatica.sh 指向命令行版本](https://www.yuque.com/woclass/bex/ubuntu#dBPzr)[OL].(2022-9-12)[2023-5-24].
[^python]: Jack.[如何将python升级到最新版本](https://bbs.deepin.org/post/246332?postId=1399722)[OL].(2022-11-22)[2023-5.25].

