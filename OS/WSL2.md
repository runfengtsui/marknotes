---
Title: WSL2 使用教程
Author: 邱彼郑楠
Date: 2023-03-10
Modified: 2025-11-24
---

# WSL2 的安装

在 Windows 上启动 `适用于 Linux 的 Windows 子系统` 功能, 使用以下命令可以列出
可以安装的发行版:
```cmd
wsl --list --online
```
以安装 Ubuntu-24.04 发行版为例, 使用以下命令:
```cmd
wsl --install -d Ubuntu-24.04
```
依次输入创建的用户名和密码, 就成功的登入了 WSL2 系统.

# WSL 迁移

WSL2 的磁盘文件默认存储在 C 盘, 位于 `C:\Users\UserName\AppData\Local\Packages\`
文件夹中. 当在 WSL2 中安装大量软件时, 这对 C 盘的磁盘容量是一个巨大考验.

* 首先将正在运行的系统关机:
```cmd
wsl --shutdown
```
* 可以使用 `wsl --list -v` 命令查看子系统状态. 在子系统关闭情况下导出全部文件:
```cmd
wsl --export Ubuntu-24.04 D:\Ubuntu2404
```
其中 `--export` 选项后的第一个参数表示子系统的名称, 这个可以在 `wsl --list -v` 
命令中查看; 后面跟的路径名称便是导出文件存储的名称.

* 导出成功后, 注销子系统:
```cmd
wsl --unregister Ubuntu-24.04
```
* 最后, 再将子系统的文件导入到新的位置, 如 `D:\WSL2\Ubuntu2404`
```cmd
wsl --import Ubuntu-24.04 D:\WSL2\Ubuntu2404 D:\Ubuntu2404
```
如果迁移后以 `root` 用户运行, 可以设置默认用户:
```cmd
Ubuntu-24.04 config --default-user username
```

# WSL2 配置

WSL2 配置当前发行版的文件为 `/etc/wsl.conf`.

## Windows 软件交互

`[interop]` 标签下可以设置 `enabled` 和 `appendWindowsPath` 来控制是否可以运行
Windows 进程以及添加 Windows 的环境变量. 为了不影响 Windows 和 WSL2 之间冲突,
均将其设置为 `false`, 重启后生效.
```conf
[interop]
enabled = false
appendWindowsPath = false
```

# USB 设备

但是 WSL2 默认不显示 USB 设备, 需要单独挂载 USB 设备.

1. 首先创建用来挂载 USB 设备的文件夹
```bash
sudo mkdir /mnt/e
```
2. 挂载
```bash
sudo mount -t drvfs E: /mnt/e
```

# Editor

在 WSL2 中使用 Neovim 编辑文件最常遇到的问题就是 `yy` 命令复制的内容无法在
Windows 下使用, 反过来 Windows 下复制的内容虽然不能通过 `p` 粘贴, 但在插入模式下
可以通过 `<Ctrl>+V` 进行粘贴. 所以需要解决的是 WSL2 中的 Neovim 和 Windows 剪贴板
之间通信的问题.

解决两者的通信需要调用 Windows 的剪贴板将 `yy` 复制的内容传送到 Windows 的剪贴板
中.
```lua
if vim.fn.has("wsl") then
    local yank = vim.api.nvim_create_augroup("YANK", { clear = true })
    vim.api.nvim_create_autocmd({ "TextYankPost " }, {
        pattern = "*",
        group = yank,
        command = ":call system('/mnt/c/windows/system32/clip.exe ', @\")"
    })
end
```

# Error

1. 错误代码 `Wsl/Service/CreateInstance/0x80040326` 导致无法正常启动子系统.
根据 [Issue #9867](https://github.com/microsoft/WSL/issues/9867), 在 PowerShell
中使用 `wsl --update` 更新子系统即可解决.

2. `/usr/lib/wsl/lib/libcuda.so.1 is not a symbolic link`.
`/usr/lib/wsl/lib/` 目录下都是文件而不是链接, 且该目录只读, 只能移到其他目录操作.
```bash
cd /usr/lib/wsl
sudo mkdir lib2
sudo ln -s lib/* lib2
sudo ldconfig
```
然后编辑文件 `/etc/ld.so.conf.d/ld.wsl.conf` 中的 `/usr/lib/wsl/lib` 修改为
`/usr/lib/wsl/lib2` 即可.
不过更改链接路径在更新驱动之后需要重新链接, 否则 `lib2` 中和 `lib` 中不一致从而
导致 WSL2 中不可使用 Windows 下的驱动.
以上操作在重启 WSL 会自动还原, 想要不被还原, 还需要修改 `/etc/wsl.conf` 中的设置
`ldconfig` 为 `false`. 这其实在 `/etc/ld.so.conf.d/ld.wsl.conf` 文件中有提示
```conf
# [automount]
# ldconfig = false
```
