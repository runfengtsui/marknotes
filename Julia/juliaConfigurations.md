---
Title: Julia 基本配置
Author: 邱彼郑楠
Date: 2023-03-14
Modified: 2023-04-01
---

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
