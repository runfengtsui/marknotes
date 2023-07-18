---
Title: Julia
Author: 邱彼郑楠
Date: 2023-03-14
Modified: 2023-07-15
---

# 安装
## juliaup

目前官方推出了 `juliaup` 这一工具可以管理 Julia 的版本, 其下载方式如下:

```bash
curl -fsSL https://install.julialang.org | sh
```

默认下载最新版本的 Julia 和 Juliaup. 使用 Juliaup 控制 Julia 的版本如:

* `juliaup update`: 安装当前版本的最新版本;
* `juliaup status`: 查看当前已经安装的版本;
* `juliaup add 1.x`: 安装指定版本;
* `juliaup default 1.x`: 设置默认启动的版本;
* `juliaup remove 1.x`: 卸载指定版本;
* `juliaup self update`: Juliaup 更新自身;
* `juliaup self uninstall`: juliaup 卸载.

## 可移植版本

如果使用 `apt` 包管理工具下载的版本过低, 可前往 [官网](https://julialang.org/downloads/) 下载 Generic Linux on x86 的 64-bit 最新版的包. 如果网络比较慢, 可以考虑使用 [清华大学开源镜像](https://mirrors.tuna.tsinghua.edu.cn/julia-releases/bin/) 下载对应版本.

```shell
wget https://julialang-s3.julialang.org/bin/linux/x64/1.9/julia-1.9.0-linux-x86_64.tar.gz
```

下载完成后, 使用 `tar -xvzf` 命令将其解压

```shell
tar -xvzf julia-1.9.0-linux-x86_64.tar.gz
```

此时 `julia-1.9.0/bin/julia` 就可以直接运行 Julia. 为了在终端任意地方使用 Julia, 将文件夹 `julia-1.9.0` 全部移至 `/opt/` 目录下(`/opt` 目录是用来安装附加软件包).

```shell
sudo mv julia-1.9.0 /opt/
```

最后一步, 建立 `/opt/julia-1.9.0/bin/julia` 的符号链接 `/usr/bin/julia`.

```shell
sudo ln -s /opt/julia-1.9.0/bin/julia /usr/bin/julia
```

这样就可以使用最新版的 `julia` 了.

> **Remark**. 删除软链接可使用以下命令
```shell
sudo rm -rf /usr/local/bin/julia
```

# 配置文件

Julia 的配置文件为 `$HOME/.julia/config/startup.jl`, 以下环境变量等可以直接在 REPL 中运行, 也可以添加到配置文件中永久保存.

## 环境变量
### 编辑器

Julia 内置一个 `edit()` 函数可以在 REPL 中使用编辑器打开文件, 可以通过环境变量来设置默认打开文件的编辑器

```Julia
ENV["JULIA_EDITOR"] = "nvim"
```

### Pkg 源

默认情况下, `Pkg` 使用 `https://pkg.julialang.org` 获取 Julia 软件包. 但大多数情况下, 国内的访问速度比较慢, 推荐使用镜像来下载软件包和更新注册表:

```julia
ENV["JULIA_PKG_SERVER"] = "https://mirrors.tuna.tsinghua.edu.cn/julia"  # 使用清华镜像
```

### Python

在安装 `PyCall` 软件包时, 需要指定 `Python` 环境:

```julia
ENV["PYTHON"] = "your/python/path"
```

更多的环境变量请参考 [环境变量](https://cn.julialang.org/JuliaZH.jl/latest/manual/environment-variables/index.html).

