---
Title: 深度操作系统
Author: 邱彼郑楠
Date: 2023-05-24
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

深度操作系统可以在 [Releases](https://github.com/neovim/neovim/releases) 上下载 `nvim.appimage` 文件直接使用 Neovim. 详细介绍见 [Neovim 的安装](./Neovim.md#Deepin).

## 配置

Neovim 的配置在 Windows 的子系统 [WSL2](./WSL2.md#Editor) 中已经做过, 相关的知识见 [Neovim 教程](./Neovim.md#Toturial), 具体的配置文件在 [NeovimConfiguration](https://gitee.com/runfengtsui/neovim-config).

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

