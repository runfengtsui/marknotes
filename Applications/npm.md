---
Title: npm 教程
Author: 邱彼郑楠
Date: 2023-05-24
Modified: 2025-11-23
---

# 安装

* 首先使用 `apt` 包管理工具安装 `npm`.

```bash
sudo apt install npm
```

得到 `npm` 版本为 5.8.0, `node` 的版本为 `10.21.0`.

* 然后使用 `npm`  安装 `n`, 由于 `apt` 安装的 `npm` 和 `node` 版本太低,会出现警告,
这在将 `npm` 和 `node` 升级之后就不会出现了.
```npm
sudo npm install n -g
```

* 最后一步, 安装最新版本的 `node` (stable 版本)
```
sudo n stable
```

可以通过 `node -v` 和 `npm -v` 查看当前 `node` 版本为 18.16.0, `npm` 版本为9.5.1.

# 镜像源

* 查看当前镜像源:
```bash
npm config get registry
```

* 设置镜像源, 如 [npmmirror 镜像站](https://npmmirror.com/):
```bash
npm config set registry https://registry.npmmirror.com
```
* 还原默认源:
```bash
npm config set registry https://registry.npmjs.org
```
