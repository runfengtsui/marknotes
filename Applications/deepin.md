---
Title: 深度操作系统
Author: 邱彼郑楠
Date: 2023-05-23
---

# Editor

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

深度操作系统是基于 Debian 的, 可以通过 `apt` 包管理工具安装 Neovim, 但这样安装的 Neovim 版本太低, 当前版本号为 `0.3.4`.

也可以像 Ubuntu 系统那样使用 PPA 添加源的方式来安装, 见 [Ubuntu 安装 Neovim](./Neovim.md##Ubuntu). 但直接使用 `add-apt-repository` 是不安全的, 还不如直接更改源文件.

没有合适的包管理工具安装的情况下, 选择直接从 [Releases](https://github.com/neovim/neovim/releases) 下载使用. 针对 Linux 可以下载两种文件, 一个是 `nvim.appimage`, 另一个是 `nvim-linux.tar.gz`. 现在更加推荐的是使用后缀名为 `appimage` 的文件, 可以免安装直接使用.

* 首先, 下载 `nvim.appimage` 文件

```bash
aria2c -s16 -x16 -k1M https://github.com/neovim/neovim/releases/download/nightly/nvim.appimage
```

* 第二步, 赋予文件 `nvim.appimage` 可执行权限:

```bash
chmod u+x nvim.appimage
```

这样, 就可以使用 `./nvim.appimage` 打开编辑器了.

但文件名 `nvim.appimage` 比较长, 而且必须在其所在的文件夹下使用, 非常不方便. 需要设置软链接方便使用 (同时为了防止 `nvim.appimage` 被误删或找不到等情况, 固定将 `nvim.appimage` 放置在 `/opt` 目录下).

```bash
# 将 nvim.appimage 移至 /opt 文件夹
sudo mv nvim.appimage /opt
cd /opt
# 增加可执行权限
chmod u+x nvim.appimage
# 设置软链接
sudo ln -s $PWD/nvim.appimage /usr/bin/nvim
```

现在, 就可以在终端的任意地方使用 `nvim` 命令了. 如果觉得 `nvim` 这个命令还比较长, 可以配置缩写如 `alias vi="nvim"` 和 `alias vim="nvim"`. 这样, `vi` 和 `vim` 命令打开的都是 Neovim.

