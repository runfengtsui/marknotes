---
Title: 深度操作系统
Author: 邱彼郑楠
Date: 2023-05-24
Modified: 2023-11-02
---

# 编辑器
## Vim 

不打算使用 Vim 编辑器, 考虑将其完全卸载, 使用 `apt` 包管理工具进行卸载:

```bash
apt -y remove vim vim-tiny vim-runtime vim-common
```

> **注意**: 如果只运行了 `apt remove vim`, `vim` 命令无法运行, 但是 `vi` 命令还是可以运行的, 因为 `vi` 命令对应的 `vim-tiny`. 至于 `vim-runtime` 和 `vim-common` 可以使用 `apt autoremove` 自动卸载.

## NeoVim

深度操作系统可以在 [Releases](https://github.com/neovim/neovim/releases) 上下载 `nvim.appimage` 文件直接使用 NeoVim. 详细介绍见 [NeoVim 的安装](../Applications/Neovim.md#深度操作系统).

## 配置

NeoVim 的配置在 Windows 的子系统 [WSL2](./WSL2.md#Editor) 中已经做过, 相关的知识见 [NeoVim 教程](../Applications/Neovim.md#教程), 具体的配置文件在 [nvim](https://gitee.com/runfengtsui/dotfiles/tree/main/nvim).

现在不需要重新配置, 只需要将原来的配置文件克隆过来即可. 配置的过程在 [dotfiles](https://gitee.com/runfengtsui/dotfiles) 仓库的 `init.sh` 脚本.

配置成功后, 打开 NeoVim, 命令模式下执行 `:PackerSync`, 安装所有插件. 插件安装完毕就配置完成了.

> **注意**. Pyright 等的安装以及 `markdown-preview.nvim` 插件需要使用 `npm` 工具, 见 [npm 的安装](../Applications/npm.md#安装). 否则 NeoVim 会提示报错.

## 默认编辑器

深度操作系统终端下的默认编辑器为 `nano`, 具体为 `/usr/bin/editor` 指向 `/etc/alternatives/editor`, 其中 `/etc/alternatives/editor` 又指向 `/usr/bin/nano`.

使用 `update-alternatives` 来控制 `editor` 感觉是比较麻烦的, 可以参考 [debian修改默认编辑器](https://www.cnblogs.com/keithtt/p/7357995.html). 主要是使用 `update-alternatives --config editor` 命令显示只有 `nano` 一个选项 (最后我把 `nano` 卸载了, `/usr/bin/editor` 以及 `/etc/alternatives/editor` 这些都没有了).

更改默认编辑器还可以通过在终端的配置文件中设置变量 `EDITOR` 来实现. 由于使用的是 [Fish Shell](../Applications/FishShell.md), 所以编辑 `~/.config/fish/config.fish` 文件, 增加语句

```bash
set -x EDITOR nvim
```

即可. 其实 `-x` 的意思是导出变量, 类似于 Bash 的 `export`.

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

Julia 的安装与配置见 [Julia的安装与配置](../Julia/julia.md).

## Python

深度操作系统自带 Python 和 Python3, 其中 Python 是 2.7.16 版本, python3 是 3.7.3 版本. 目前 Python3 版本已经来到 3.12 系列, 3.7 已经显得有点老了, 所以需要安装新版本使用.

> **注意** 不要尝试更新系统自带的 Python 和 Python3, 这样会使得系统崩溃. 如果想要使用其他版本的 Python3, 可以使用虚拟环境隔离[^python].

> 选择使用 [Poetry](https://python-poetry.org/) 这一工具来管理多版本的 Python. 详细见 [Poetry 教程](../Python/Poetry.md).

首先, 从 [官网](https://www.python.org/) 进入 [下载页面](https://www.python.org/downloads/) 下载所需版本的安装包.

下载的文件是 `tgz` 格式, 解压缩

```shell
tar -xvf Python-3.11.4.tgz
```

进入解压缩后的文件夹, 运行 `./configure`, 同时设置安装目录 (`--prefix`), 设置共享 (`--enable-shared`) 以及开启优化 (`--enable-optimizations`).

```shell
cd Python-3.11.4
./configure --prefix=/opt/python3.11 --enable-shared --enable-optimizations
```

然后, 使用 `make` 编译并进行安装

```shell
make
sudo make install
```

但这样并不能运行起来 `Python3.11`, 会提示缺少文件 `libpython3.11.so.1.0`, 所以还需要将 `lib` 文件夹下的这一文件复制到 `/usr/lib/` 和 `/usr/lib64/` 文件夹中.

```shell
sudo cp /opt/python3.11/lib/libpython3.11.so.1.0 /usr/lib/
sudo cp /opt/python3.11/lib/libpython3.11.so.1.0 /usr/lib64/
```

这样 Python3.11 就可以成功启动. 如果想要再任意地方启动 Python3.11, 还需要设置符号链接

```shell
sudo ln -s /opt/python3.11/bin/python3.11 /usr/bin/python3.11
sudo ln -s /opt/python3.11/bin/pip3.11 /usr/bin/pip3.11
```

如果在编译过程中缺少其他依赖, 可以参考 [官方安装说明](https://devguide.python.org/getting-started/setup-building/index.html#install-dependencies) 或者 [在deepin系统下安装python3.8](https://bbs.deepin.org/post/254748).

### Python 开发包

深度操作系统默认没有装 Python 的开发包, 因此如果使用 C++ 调用 Python 时是找不到 `Python.h` 这个头文件的. 这就需要自己安装 Python 的开发包[^Python.h].

深度操作系统默认的 Python3 版本为 Python3.7, 选择安装 Python3.7 的开发包, 使用 `apt` 包管理工具进行安装:

```bash
sudo apt install python3.7-dev
```

安装得到的头文件都在目录 `/usr/include/python3.7m/` 下. 此时就可以使用 C++ 调用 Pyhton 程序了.

### 多版本下 tkinter 出错

深度操作系统默认的 Python3 想要使用 `tkinter` 需要使用 `apt` 安装 `python3-tk`:

```shell
sudo apt install python3-tk
```

同时安装了多个版本的 Python, 从 `python3-tk` 的描述中可以看出其是对所有的 Python3 版本都应该支持的. 但是其他版本调用 `tkinter` 会出现以下错误:

```
import _tkinter # if this fails your Python may not be configured for TK
importError: No module named _tkinter
```

出错的原因是没有安装 `Toolkit for Tcl and X11 (default version) - development files`[^tkinter]. 使用 `apt` 进行安装:

```shell
sudo apt install tk-dev
```

然后删除原来的版本, 重新按照 [Python](##Python) 的编译步骤重新编译即可正常使用 `tkinter` 了.

[^baltam]: woclass.[将 baltamatica.sh 指向命令行版本](https://www.yuque.com/woclass/bex/ubuntu#dBPzr)[OL].(2022-9-12)[2023-5-24].
[^python]: Jack.[如何将python升级到最新版本](https://bbs.deepin.org/post/246332?postId=1399722)[OL].(2022-11-22)[2023-5.25].
[^Python.h]: 拾依H.[Python.h: No such file or directory错误解决](https://zhuanlan.zhihu.com/p/613210828)[OL].(2023-3-11)[2023-6-5].
[^tkinter]: lovepython1314.[Deepin-linux下的多版本python间安装tkinter出错之分析](https://blog.csdn.net/weixin_40840880/article/details/103038818)[OL].(2019-11-12)[2023-11-2].

