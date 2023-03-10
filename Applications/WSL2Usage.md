---
Title: WSL2使用教程
Author: 邱彼郑楠
Date: 2023-03-10
---

# WSL2 的安装

根据微软的官方文档 [使用 WSL 在 Windows 上安装 Linux](https://learn.microsoft.com/zh-cn/windows/wsl/install#step-1---enable-the-windows-subsystem-for-linux), 现在在 Windows 上安装 WSL 只需要在 PowerShell 或 Windows 命令提示符使用如下命令

```powershell
wsl --install
```

运行如图所示

![alt=WSL安装信息](../imgs/wsl_install_info.png)

根据提示重启计算机后, WSL 会自动启动

![alt=创建用户](../imgs/wsl_create_username.png)

依次输入创建的用户名和密码, 就成功的登入了 WSL 系统.

这个系统即使你退出终端后台仍在运行, 想要关闭需要在 PowerShell 或 Windows 命令提示符中输入

```powershell
wsl --shutdown
```

# 包管理工具

WSL2 安装的是 Ubuntu 系统, 使用 `apt` 这一包管理工具.

想要查找可以安装的软件包可使用如下命令

```bash
apt-cache search package_name
```

如果想要显示软件包的详细信息, 使用如下命令

```bash
apt-cache show package_name
```

以上内容参考 [Ubuntu系统如何搜索要安装的软件包](https://blog.csdn.net/aaa123524457/article/details/96865138).

# Fish 终端

如果不要求安装最新版的 Fish, 使用

```bash
sudo apt-get install fish
```

即可. 安装的是 3.3.1 版本, 目前 [官网](https://fishshell.com/) 最新版本是 3.6.0.

## 设置 Fish Shell 为默认 Shell

使用 `chsh` 命令可以设置默认 Shell

```bash
chsh -s /usr/bin/fish
```

重启终端, 此时打开的就是 Fish Shell.

如果想要重新设置默认 Shell 为 Bash，使用类似的命令

```bash
chsh -s /usr/bin/bash
```

参考 [window安装 Ubuntu子系统 和 fish](https://blog.csdn.net/chengler/article/details/119613219).

# USB 设备

我的电脑有两个盘, 平时使用 USB 设备存储一些文件, 但是 WSL2 默认不显示 USB 设备, 这需要挂载 USB 设备.

1. 首先建一个用来挂载 USB 设备里面文件的文件夹

```bash
sudo mkdir /mnt/e
```

2. 挂载

```bash
sudo mount -t drvfs E: /mnt/e
```

这样就可以在 WSL2 中访问 USB 设备了.

这一部分内容参考 [WSL2挂载USB设备](https://blog.csdn.net/qq_59475883/article/details/123314000).
