---
Title: Julia 基本配置
Author: 邱彼郑楠
Date: 2023-03-14
Modified: 2023-04-04
---

# 安装

如果使用 `apt` 包管理工具下载的版本过低, 可前往 [下载页面](https://julialang.org/downloads/) 查看最新版的 Julia, 复制最新版的下载地址下载,

```shell
wget https://julialang-s3.julialang.org/bin/linux/x64/1.8/julia-1.8.5-linux-x86_64.tar.gz
```

下载完成后, 使用 `tar -xvzf` 命令将其解压

```shell
tar -xvzf julia-1.8.5-linux-x86_64.tar.gz
```

`/opt` 目录是用来安装附加软件包, 将解压得到的 `julia-1.8.5` 文件加拷贝到 `/opt` 文件夹中

```shell
sudo cp -r julia-1.8.5 /opt/
```

最后一步, 建立 `/opt/julia-1.8.5/bin/julia` 的软链接

```shell
sudo ln -s /opt/julia-1.8.5/bin/julia /usr/local/bin/julia
```

这样就可以使用最新版的 `julia` 了.

> **Remark**. 删除软链接可使用以下命令
```shell
sudo rm -rf /usr/local/bin/julia
```

# 环境变量
## 编辑器

Julia 内置一个 `edit()` 函数可以在 REPL 中使用编辑器打开文件, 可以通过环境变量来设置默认打开文件的编辑器

```Julia
ENV["JULIA_EDITOR"] = "nvim"
```

## Pkg 源

默认情况下, `Pkg` 使用 `https://pkg.julialang.org` 获取 Julia 软件包. 但大多数情况下, 国内的访问速度比较慢, 推荐使用镜像来下载软件包和更新注册表:

```julia
ENV["JULIA_PKG_SERVER"] = "https://mirrors.tuna.tsinghua.edu.cn/julia"  # 使用清华镜像
```

## Python

在安装 `PyCall` 软件包时, 需要指定 `Python` 环境:

```julia
ENV["PYTHON"] = "your/python/path"
```

以上环境变量可以直接在 REPL 中设置. 而如果想要保持这个设置, 需要将其写入 `~/.julia/config/startup.jl` 文件中.

更多的环境变量请参考 [环境变量](https://cn.julialang.org/JuliaZH.jl/latest/manual/environment-variables/index.html).
