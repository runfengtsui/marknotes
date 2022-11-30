---
Title: Ubuntu 系统 NeoVim 的安装与使用
Author: 邱彼郑楠
Date: 2022-10-13
Modified: 2022-11-30
---

# NeoVim 的安装
## Ubuntu 系统安装 NeoVim

使用 `apt` 在我的阿里云服务器上安装 NeoVim： 

```bash
sudo apt install neovim
```

但是安装的版本是 0.4.3, 想要使用 Lua 对 NeoVim 进行配置需要 NeoVim >= 0.5. 因此考虑使用 PPA 方法安装 NeoVim。

在使用 PPA 安装之前，需要安装如下依赖项：

```bash
sudo apt install software-properties-common -y
```

安装好了依赖项之后，导入 PPA。NeoVim PPA 团队提供了两种选择，即稳定版本的和不稳定版本的。选择稳定的 NeoVim PPA 进行导入：

```bash
sudo add-apt-repository ppa:neovim-ppa/stable -y
```

运行 APT 更新以同步更改：

```bash
sudo apt-get update
```

然后，就可以使用最初的命令安装 NeoVim 了，安装的 NeoVim 版本为 0.7.3. 

# NeoVim 的基本配置

在 NeoVim 中，有一组函数可以设置 Vim 属性，分别为

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

但是这些函数的名字都很长，用起来很不方便。NeoVim 又对上述函数进一步封装，提供了一组元访问器，从而可以通过变量赋值的方式设置 Vim 属性。对应于全局属性、窗口属性和缓冲区属性，元访问器有三种访问对象 `vim.o`, `vim.wo` 和 `vim.bo`. 例如 `vim.o.number = true` 命令就是设置行号，其他的类似。

## 快捷键绑定

设置快捷键可以方便 NeoVim 的使用。NeoVim 定义了如下函数可以定义、获取和删除快捷键：

```lua
vim.api.nvim_set_keymap()   -- 设置快捷键
vim.api.nvim_get_keymap()   -- 获取快捷键
vim.api.nvim_del_keymap()   -- 删除快捷键
```

设置快捷键的方式如下：

```lua
vim.api.nvim_set_keymap(模式, 映射键位, 执行命令, 其他属性)
```

其中模式参数为空字符串时表示全模式下，模式参数为 `n`, `i`, `v`, `s` 和 `c` 时分别对应着 Vim 的正常模式、插入模式、可视模式、选择模式、命令模式。其他属性一般设置两个属性 `noremap` 和 `silent`。设置 `noremap` 为 `true` 表示禁止递归，关于快捷键递归的讨论可以参考[从零开始配置vim(3)————键盘映射进阶](https://zhuanlan.zhihu.com/p/541017886)，这篇文章详细讨论了使用递归会带来的结果。`silent` 属性设置为 `true` 表示执行命令时不回显内容。

为了方便设置快捷键，可以通过设置局部变量来减少输入的一长串 `vim.api.nvim_set_keymap`.

```lua
local map = vim.api.nvim_set_keymap
local opts = { noremap = true, silent = true }
```

如此，以后设置快捷键就这样使用：

```lua
map("i", "jk", "<Esc>", opts)
```

由于 NeoVim 自身还有安装的插件都带有按键映射，所以当按键映射过多时，没有合适的按键可以选择。这时候，可以考虑设置 `leader` 键，然后通过 `<leader>` 加其他按键的方式设为快捷键。

同样可以使用元访问器简单地设置，如设置空格键为 `<leader>` 键：

```lua
vim.g.mapleader = " "
```

## 自动命令

对于 Markdown 和 HTML 文件设置不自动换行，

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

使用关键字 `augroup` 创建一个自动命令组。`autocmd!` 可以清除同一组之前的命令。

使用自动命令，只要配置文件被保存，就自动加载

```vim
augroup NVIMRC
    autocmd!
    autocmd BufWritePost init.vim source %
augroup END
```

## 插件的安装与配置
### NvimTree 文件树

NeoVim 自带一个目录管理 `netrw`，但其功能有限且不美观，所以可以选择使用 `NvimTree` 作为目录管理插件。在 `lua/plugins.lua` 配置文件中添加以下内容：

```lua
-- nvim-tree
use {
    'kyazdani42/nvim-tree.lua',
    requires = 'kyazdani42/nvim-web-devicons', -- optional, for file icons
    tag = 'nightly' -- optional, updated every week. (see issue #1193)
}
```

保存，然后自动运行 `PackerSync` 命令进行安装。安装完成后，该插件提供了 `NvimTreeToggle` 命令打开文件树。打开之后发现每个文件前面都有一个小方框，这应该是文件的图标没有显示出来。在安装插件的时候我们已经安装了图标的支持，即 `nvim-web-devicons`。[NvimTree](https://github.com/nvim-tree/nvim-tree.lua) 和 [Nvim-web-devicons](https://github.com/nvim-tree/nvim-web-devicons)的文档都标注了需要安装 Nerd 字体。从 [Nerd Fonts](https://www.nerdfonts.com/) 的官网选择喜欢的字体下载，然后安装。

下面开始对 NvimTree 插件进行配置。首先，可以通过 `vim.g.loaded` 和 `vim.g.loaded_netrwPlugin` 禁用 `netrw` 插件。其他配置选项可以通过 `help nvim-tree-setup` 命令查看，选择合适的配置。我的配置如下：

```lua
require 'nvim-tree'.setup {
    -- Change how files within the same directory are sorted.
    sort_by = "case_sensitive",
    view = {
        -- Resize the window on each draw based on the longest line.
        adaptive_size = true,
    },
    filters = {
        -- Custom list of vim regex for file/directory names that will not be shown.
        custom = { "^\\.git" },
        -- List of directories or files to exclude from filtering: always show them.
        exclude = { ".gitignore" },
    },
}
```

其中 `sort_by` 是文件树中文件(夹)排序方式，`adaptive_size` 可以自动调节文件树的窗口大小，`custom = { "^\\.git" }` 使用正则表达式匹配到 `.git` 文件夹并不在文件中显示该文件夹，也可以添加其他想要忽略掉的文件夹，比如忽略掉点文件夹可以在 `filters` 中设置 `dotfiles = true`。但是使用正则表达式匹配 `.git` 会把 `.gitignore` 文件也隐藏，所以需要添加 `exclude = { ".gitignore" }`，即不管 `dotfiles` 和 `exclude` 如何设置，始终显示 `.gitignore` 文件。

最后，只需要设置一个快捷键，将 `NvimTreeToggle` 绑定到 `<Alt-m>` 上方便打开或关闭文件树。其实我很想知道如何设置打开文件后自动打开文件树，但没有找到相关的内容。

### bufferline 标签页插件

`bufferline` 插件可以将每一个缓冲区当成一个标签页，并且使得 Neovim 的标签页更加的好看。根据 [bufferline](https://github.com/akinsho/bufferline.nvim) 的文档，安装 `bufferline` 插件只需要在 `packer` 插件管理器中添加如下内容：

```lua
use {
    'akinsho/bufferline.nvim',
    tag = "v2.*",
    requires = 'kyazdani42/nvim-web-devicons'
}
```

其中 `tag = "v2.*"` 只适用于版本在 0.6.1 之上的 Nvim，而对于版本为 0.6.1 甚至更低的版本，应该使用 `tag = v1.*"`. 关于其安装的说明可以参考 [Installation](https://github.com/akinsho/bufferline.nvim#Installation).

安装成功后，创建并打开 `lua/plugin-config/bufferline.lua` 文件，然后对 `bufferline` 插件进行配置。根据[Usage](https://github/akinsho/bufferline.nvim#Usage)的说明，必须将 `vim.opt.termguicolors` 设置为 `true`. 命令模式下使用 `h bufferline-configuration` 查看配置说明，我们大部分采用默认配置，这里着重添加上打开 `NvimTree` 时标签显示的偏移，即

```lua
vim.opt.termguicolors = true
require('bufferline').setup{
    options = {
        -- 左侧让出 nvim-tree 的位置
        offsets = {{
            filetype = "NvimTree",
            text = "File Explorer", -- 显示文本 File Explorer
            highlight = "Directory",-- 高亮文件夹，将文件夹和文件区分
            text_align = "left"
        }},
    }
}
```

最后需要配置的是快捷键，常用的有标签页的切换以及关闭当前标签页(缓冲区)。对于标签页的切换，`bufferline` 提供了 `BufferLineCyclePre` 和 `BufferLineCycleNext` 两个命令可以切换标签页，我分别将 `Alt-h` 和 `Alt-l` 的组合映射为以上两个命令。`bufferline` 还提供了 `BufferLinePick` 命令配合 `buffer_id` 快速切换标签页。

对于关闭当前标签页(缓冲区), `bufferline` 提供了 `BufferLinePickClose` 命令，运行该命令后，每一个标签页上都会出现一个 `buffer_id` 供选择，再按相应字母或数字就可以关闭对应的标签页。另外，内置的缓冲区命令 `bdelete %` 可以关闭当前缓冲区。但如果同时打开多个标签页，在不打开 `NvimTree` 的情况下，是没有问题的；打开 `NvimTree` 再使用上述命令关闭当前标签页，会出现除 `NvimTree` 以外的所有窗口都被关闭，此时的其他文件的缓冲区并未关闭。

为了解决上述问题，根据 [请问有没有解决bufferline和nvim tree会关闭所有buffer得问题](https://github.com/nshen/learn-neovim-lua/issues/14) 中提供的解决方案，可以在安装 `bufferline` 插件的同时，安装 [vim-bbye](https://github.com/moll/vim-bbye) 插件。即在 `require` 一项中添加 `moll/vim-bbye` 即可。

```lua
use {
    'akinsho/bufferline.nvim',
    tag = "v2.*",
    requires = {'kyazdani42/nvim-web-devicons', 'moll/vim-bbye'}
}
```

`vim-bbye` 插件提供了 `Bdelete` 命令在不关闭当前窗口的前提下关闭缓冲区。安装好 `vim-bbye` 插件后，在 `bufferline` 插件的配置文件中将 `close_command` 和 `right_mouse_command` 均设置为 `Bdelete! %d`，即

```lua
vim.opt.termguicolors = true
require('bufferline').setup{
    options = {
        -- 关闭标签页的命令
        close_command = "Bdelete! %d",
        right_mouse_command = "Bdelete! %d",
        offsets = {{
            filetype = "NvimTree",
            text = "File Explorer",
            highlight = "Directory",
            text_align = "left"
        }},
    }
}
```

习惯于用 `Ctrl` 和 `w` 的组合关闭页面，我将其映射为 `Bdelete %` 就可以方便的关闭标签页了。这样 `bufferline` 就配置完成了。

最后对于 `bufferline` 的配置补充的一点是，还没有找到当所有文件都关闭时，NvimTree 也自动关闭的很好的解决方案。

### lualine 状态栏插件

不使用插件也是可以配置 NeoVim 的状态栏的，详细可以参考 [从零开始配置 vim(15)————状态栏配置](https://zhuanlan.zhihu.com/p/554641028) 这篇文章的前半部分。当然，也可以使用 [lualine](https://github.com/nvim-lualine/lualine.nvim) 插件快速美化状态栏。

将下述代码插入到 `packer.nvim` 插件管理的配置文件 `lua/plugins.lua` 中：

```lua
-- lualine
use {
    'nvim-lualine/lualine.nvim',
    requires = { 'kyazdani42/nvim-web-devicons', opt = true }
}
```

`lualine` 的初始化配置已经可以了，由于前面设置了主题为 `tokyonight`，所以在初始化配置中添加 `theme = "tokyonight"` 即可。另外，我参考了 [evil_lualine](https://github.com/nvim-lualine/lualine.nvim/bolb/master/examples/evil_lualine.lua) 这个配置，在我的配置中添加了 `filesize`、`diagnostics` 和 `LSP` 的内容使其更加丰富。

### toggleterm 终端插件


这个时候，[toggleterm](https://github.com/akinsho/toggleterm.nvim) 终端插件很好的实现了我想要的布局。使用 `Packer` 插件管理器安装 `toggleterm` 插件：

```lua
-- toggleterm
use {
    'akinsho/toggleterm.nvim',
    tag = 'v2.*'
}
```

安装完成后，创建配置文件 `plugin-config/toggleterm.lua`。没有特别的需求的话直接使用默认配置就可以了，该插件提供的终端打开即为插入模式，输入 `exit` 即可退出终端退出缓冲区同时退出窗口。这里参照 [从零开始配置vim(19)————终端模式](https://zhuanlan.zhihu.com/p/559747798) 配置了 `IPython` 和 `Julia` 语言的终端如下：

```lua
local Terminal = require('toggleterm.terminal').Terminal
local pyterm = Terminal:new({
    cmd = 'ipython',
    direction = 'horizontal'
})
function python_toggle()
    pyterm:toggle()
end
vim.api.nvim_set_keymap("n", "<leader>py", "<Cmd>lua python_toggle()<CR>", {noremap = true, silent = true})

local juliaterm = Terminal:new({
    cmd = 'julia',
    direction = 'horizontal'
})
function julia_toggle()
    juliaterm:toggle()
end
vim.api.nvim_set_keymap(
    "n",
    "<leader>j",
    "<Cmd>lua julia_toggle()<CR>",
    { noremap = true, silent = true }
)
```

这里面 `direction` 设置为 `horizontal` 是可以方便逐句执行代码，因为 `toggleterm` 是可以将语句传入到终端中。
