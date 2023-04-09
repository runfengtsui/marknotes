---
Title: Fish 终端的安装与使用
Author: 邱彼郑楠
Date: 2023-03-14
Modified: 2023-04-09
---

# Fish安装

可以直接使用 Ubuntu 系统的包管理工具 `apt` 进行安装 `sudo apt install fish`, 但这样安装的不是最新版本. 可以前往 [官网](https://fishshell.com/) 查看最新版本.

根据 Fish Shell 维护团队给出的 [PPA description](https://launchpad.net/~fish-shell/+archive/ubuntu/release-3), 安装最新版的 Fish Shell 只需要运行以下命令:

```bash
sudo apt-add-repository ppa:fish-shell/release-3
sudo apt update
sudo apt install fish
```

这样最新版的 Fish Shell 就安装好了.

# 设置Fish为默认终端

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

# 配置文件

* 添加环境变量 `set -x PATH path $PATH`
