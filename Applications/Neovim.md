---
Title: NeoVim 的安装与配置教程
Author: 邱彼郑楠
Date: 2022-10-13
Modified: 2023-07-16
---

# 安装
## Windows

从 [Releases](https://github.com/neovim/neovim/releases) 页面下载适合电脑的 `nvim-win64.zip` 压缩文件, 解压缩后, 直接可以运行里面的 `nvim.exe` 或 `nvim-qt.exe` 命令. 建议将解压缩后的文件夹添加到系统路径, 这样可以在任何位置直接使用.

在 Windows 系统下, NeoVim 的配置文件在 `~\AppData\Local\nvim` 中. 由于这个文件的路径比较长, 如果想像 Vim 一样将配置文件放置在 `~\vimfiles` 中, 需要将两个路径建立一个软链接:

```powershell
New-Item -ItemType SymbolicLink -Path .\AppData\Local\nvim -Value .\vimfiles
```

上述 PowerShell 命令需要在根目录 `~` 下运行, 另外需要注意 `.\vimfiles` 文件夹是需要存在的. 

## Ubuntu

使用 `sudo apt install neovim` 命令在 Ubuntu 系统上安装 NeoVim, 安装的版本比较老旧. 想要安装新版本的 NeoVim, 需要使用 PPA 方法安装.

导入 PPA, NeoVim PPA 团队提供了 `stable` 版和 `unstable` 版, 其中 `unstable` 版是最新版本.

```bash
sudo add-apt-repository ppa:neovim-ppa/unstable -y
```

如果无法成功导入 PPA, 可能是缺少依赖项, 先执行命令安装依赖项:

```bash
sudo apt install software-properties-common -y
```

依赖项安装成功后, 再次执行 `sudo add-apt-repository ppa:neovim-ppa/unstable -y`, 成功导入便可进行更新：

```bash
sudo apt-get update
```

更新完毕后, 使用 `sudo apt-get install neovim` 安装即可.

## 深度操作系统

深度操作系统是基于 Debian 的, 可以通过 `apt` 包管理工具安装 Neovim, 但这样安装的 Neovim 版本太低, 当前版本号为 `0.3.4`.

也可以像 Ubuntu 系统那样使用 PPA 添加源的方式来安装, 见 [Ubuntu 安装 Neovim](#Ubuntu). 但直接使用 `add-apt-repository` 是不安全的, 还不如直接更改源文件.

没有合适的包管理工具安装的情况下, 有两种选择使用 NeoVim.

### 源码编译

采用源码编译安装 NeoVim 需要满足以下条件且有预置的工具:

* `Clang` 或者 `GCC` 版本 4.9 以上;
* `CMake` 版本 3.10 以上, 且有 `TLS/SSL` 支持.

使用 `apt` 安装必要的依赖:

```bash
sudo apt install ninja-build gettext cmake unzip curl
```

克隆一份源码到本地, 进入文件夹后切换到 `stable` 版

```git
git clone git@github.com:neovim/neovim.git
git checkout stable
```

使用 `make` 进行编译, 设置安装路径为 `/opt/nvim`

```bash
make CMAKE_BUILD_TYPE=RelWithDebInfo CMAKE_INSTALL_PREFIX=/opt/nvim
```

再使用 `make` 进行安装

```bash
sudo make install
```

最后在文件夹 `/opt/nvim/bin/` 下将 `nvim` 链接到 `/usr/bin` 文件夹下使得在任意地方都可以使用

```bash
sudo ln -s /opt/nvim/bin/nvim /usr/bin/nvim
```

### 便携版本

可以直接从 [Releases](https://github.com/neovim/neovim/releases) 下载针对 Linux 的两种便携版本, 一个是 `nvim.appimage`, 另一个是 `nvim-linux.tar.gz`. 现在更加推荐的是使用后缀名为 `appimage` 的文件, 可以免安装直接使用.

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

## 更新

Ubuntu 系统的 NeoVim 如果是使用 PPA 方法安装, 则运行 `apt update` 和 `apt upgrade` 命令就会自动更新到最新版本.

否则, 不管是 Windows 系统还是深度操作系统, 都可以删除掉原来下载好的文件, 参照 [安装](#安装) 重新下载最新的文件放在原来的位置即可. 其中

* Windows 系统对应于 `nvim-win64.zip` 文件;
* 深度操作系统对应于 `nvim.appimage` 文件.

# 教程
## 自动命令

对于 Markdown 和 HTML 文件设置不自动换行, 

```vim
autocmd BufNewFile, BufReadPost *.html setlocal nowrap
```

或者使用 FileType 改写上述命令

```vim
autocmd FileType html setlocal nowrap
```

根据不同语言定义快捷键快速添加注释

```vim
autocmd FileType python nnoremap <buffer> <localleader>c I#<esc>
autocmd FileType javascript nnoremap <buffer> <localleader>c I//<esc>
```

### 自动命令组

使用关键字 `augroup` 创建一个自动命令组. `autocmd!` 可以清除同一组之前的命令. 

使用自动命令, 只要配置文件被保存, 就自动加载

```vim
augroup NVIMRC
    autocmd!
    autocmd BufWritePost init.vim source %
augroup END
```

# 配置
## 取消注释换行自动添加注释符

在使用 NeoVim 编写代码时, 如果本行是注释行, 换行之后会自动在行首添加注释符. 这在使用多行注释时是非常方便的, 而使用单行注释就需要每次删掉注释符. 

可以找到针对 lua 语言取消自动注释的内容[^lspconfig], 自然对于其他语言也是也是类似的, 但不能每一种语言都配置一遍. 同样可以找到取消自动注释的自动命令[^autocomment], 可以创建[自动命令](#自动命令)针对特定的语言或者所有文件类型都取消自动注释.
[^lspconfig]: Masimaro.[从零开始配置vim(23)——lsp基础配置](https://zhuanlan.zhihu.com/p/562050115)[OL].(2022-9-7)[2023-7-16].
[^autocomment]: 疯流人物.[让vim不要自动添加新的注释行](https://blog.csdn.net/u013408061/article/details/77774020)[OL].(2022-12-7)[2023-7-16].

将 VimScripts 中的自动命令用 NeoVim 提供的 API 改写[^packer], 以下内容添加到 `lua\autocmd.lua` 配置文件中：
[^packer]: Masimaro.[从零开始配置 vim(11)——插件管理](https://zhuanlan.zhihu.com/p/551941252)[OL].(2022-8-10)[2023-7-16].

```lua
local disable_auto_comment = vim.api.nvim_create_augroup("DISABLE_AUTO_COMMENT", { clear = true })
vim.api.nvim_create_autocmd({"FileType"}, {
    pattern = "*",
    group = disable_auto_comment,
    callback = function()
        vim.opt_local.formatoptions = vim.opt_local.formatoptions - {"r", "c", "o"}
    end
})
```

保存后, 再打开新的文件就不会出现自动注释的问题了. 

## 快速注释

首先说明一下可视化模式快捷键 `<Ctrl>+v` 在 Windows 电脑下失效的问题[^disablectrlv].
[^disablectrlv]: 亮子AI.[【vim】可视化模式快捷键 Ctrl + v 不起作用了](https://blog.csdn.net/henryhu712/article/details/123298423)[OL].(2022-3-5)[2023-7-16].

由于 `<Ctrl>+v` 在 Windows 电脑下是粘贴功能, 该快捷键不起作用. 可以使用 `<Ctrl>+q` 快捷键进入 `Visual Block` 模式.

下面将说明如何进行多行注释[^comment].
[^comment]: yongxinz.[Vim 编辑器｜批量注释与批量取消注释](https://juejin.cn/post/7041783262544396296)[OL].(2021-12-15)[2023-7-16].

`<Ctrl>+q` 快捷键进入 `Visual-Block` 模式, 方向键选择要注释的行, 按下大写字母 `I` 在行首插入, 输入注释的字符如 `//`, `#` 等, 最后按下 `<Esc>` 即可.

相应地, 取消注释也需要进入 `Visual-Block` 模式, 方向键选中所有要取消注释行的注释字符, 按下 `x` 或者 `d` 删除这些字符即可.





在 NeoVim 中, 有一组函数可以设置 Vim 属性, 分别为

```
-- 设置全局属性
vim.api.nvim_set_option()
vim.api.nvim_get_option()
-- 设置窗口属性
vim.api.nvim_win_set_option()
vim.api.nvim_win_get_option()
-- 设置缓冲区属性
vim.api.nvim_buf_set_option()
vim.api.nvim_buf_get_option()
```

但是这些函数的名字都很长, 用起来很不方便. NeoVim 又对上述函数进一步封装, 提供了一组元访问器, 从而可以通过变量赋值的方式设置 Vim 属性. 对应于全局属性、窗口属性和缓冲区属性, 元访问器有三种访问对象 `vim.o`, `vim.wo` 和 `vim.bo`. 例如 `vim.o.number = true` 命令就是设置行号, 其他的类似. 

## 快捷键绑定

设置快捷键可以方便 NeoVim 的使用. NeoVim 定义了如下函数可以定义、获取和删除快捷键：

```lua
vim.api.nvim_set_keymap()   -- 设置快捷键
vim.api.nvim_get_keymap()   -- 获取快捷键
vim.api.nvim_del_keymap()   -- 删除快捷键
```

设置快捷键的方式如下：

```lua
vim.api.nvim_set_keymap(模式, 映射键位, 执行命令, 其他属性)
```

其中模式参数为空字符串时表示全模式下, 模式参数为 `n`, `i`, `v`, `s` 和 `c` 时分别对应着 Vim 的正常模式、插入模式、可视模式、选择模式、命令模式. 其他属性一般设置两个属性 `noremap` 和 `silent`. 设置 `noremap` 为 `true` 表示禁止递归, 关于快捷键递归的讨论可以参考[从零开始配置vim(3)————键盘映射进阶](https://zhuanlan.zhihu.com/p/541017886), 这篇文章详细讨论了使用递归会带来的结果. `silent` 属性设置为 `true` 表示执行命令时不回显内容. 

为了方便设置快捷键, 可以通过设置局部变量来减少输入的一长串 `vim.api.nvim_set_keymap`.

```lua
local map = vim.api.nvim_set_keymap
local opts = { noremap = true, silent = true }
```

如此, 以后设置快捷键就这样使用：

```lua
map("i", "jk", "<Esc>", opts)
```

由于 NeoVim 自身还有安装的插件都带有按键映射, 所以当按键映射过多时, 没有合适的按键可以选择. 这时候, 可以考虑设置 `leader` 键, 然后通过 `<leader>` 加其他按键的方式设为快捷键. 

同样可以使用元访问器简单地设置, 如设置空格键为 `<leader>` 键：

```lua
vim.g.mapleader = " "
```

