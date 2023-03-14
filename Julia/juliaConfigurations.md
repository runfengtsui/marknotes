---
Title: Julia 基本配置
Author: 邱彼郑楠
Date: 2023-03-14
---

# 环境变量

Julia 内置一个 `edit()` 函数可以在 REPL 中使用编辑器打开文件, 可以通过环境变量来设置默认打开文件的编辑器

```Julia
ENV["JULIA_EDITOR"] = "nvim"
```

该环境变量可以直接在 REPL 中设置. 而如果想要保持这个设置, 需要将其写入 `~/.julia/config/startup.jl` 文件中.

更多的环境变量请参考 [环境变量](https://cn.julialang.org/JuliaZH.jl/latest/manual/environment-variables/index.html).
