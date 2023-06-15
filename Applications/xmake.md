---
Title: xmake
Author: 邱彼郑楠
Date: 2023-06-05
---

* [Gitee 仓库](https://gitee.com/tboox/xmake)
* [Github 仓库](https://github.com/xmake-io/xmake) 
* [官网](https://xmake.io/#/zh-cn/) 

# 安装

使用 `curl` 进行安装

```bash
curl -fsSL https://xmake.io/shget.text | bash
```

或者使用 `wget` 进行安装

```bash
wget https://xmake.io/shget.text -O - | bash
```

# 常用命令

* `add_rules("mode.debug", "mode.release")` - 可选配置, 用于描述编译模式, 默认情况下会采用 `release` 编译模式.
* `target("hello")` - 定义一个目标程序.
* `set_kind("binary")` - 指定编译生成的目标程序是可执行的.
* `add_files("src/*.cpp")` - 添加 `src` 目录下的所有 C++ 源文件.
