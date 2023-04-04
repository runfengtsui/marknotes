---
Title: Fish 终端的安装与使用
Author: 邱彼郑楠
Date: 2023-03-14
---

# Fish安装

直接使用 Ubuntu 系统的包管理工具就可以安装

```bash
sudo apt-get install fish
```

但这样安装的不是最新版本. 可以前往 [官网](https://fishshell.com/) 查看最新版本.

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
