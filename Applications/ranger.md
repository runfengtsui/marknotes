---
Title: ranger
Author: 邱彼郑楠
Date: 2023-06-08
---

# 安装

直接使用 `apt` 包管理工具进行安装:

```bash
sudo apt install ranger
```

# 配置
## 图标

[ranger_devicons](https://github.com/alexanderjeurissen/ranger_devicons) 项目提供了 `ranger` 的图标插件. 该插件使用的图标依赖于 Nerd Fonts, 这种字体实际上在配置 Neovim 里的图标时已经使用了.

将该项目克隆到 `~/.config/ranger/plugins/` 文件夹下, 再在配置文件 `~/.config/ranger/rc.conf` 中添加语句 `default_linemode devicons`:

```bash
git clone git@github.com:alexanderjeurissen/ranger_devicons.git ~/.config/ranger/plugins/ranger_devicons
echo "default_linemode devicons" >> $HOME/.config/ranger/rc.conf
```

理论上, 之后再打开 `ranger` 文件管理器, 文件名之前都会出现一个对应文件类型的图标. 但实际上, 输入命令 `ranger --debug` 之后, 会提示报错

```
Exception: Invalid linemode: devicons; should be filename/metatitle/permissions/fileinfo/mtime/sizemtime
```

根据 [Issue 64](https://github.com/alexanderjeurissen/ranger_devicons/issues/64), 提供了一种解决方案是将 `plugins/ranger_devicons` 文件夹下的 Python 文件都移动到 `plugins/` 目录下. 这样确实解决了问题.

## 语法高亮

在 `ranger` 下预览文件时, 只需要安装 `highlight` 就可以实现预览的语法高亮[^rangerconfig]

```bash
sudo apt install highlight
```

## 绘制边框

在配置文件 `rc.conf` 中, 将 `set draw_borders none` 改为 `true` 即可实现每一层目录都显示一个方框[^rangerconfig].

[^rangerconfig]: 赵赛赛.[ranger配置与使用](https://www.zssnp.top/2021/06/03/ranger/)[OL].(2022-9-18)[2023-6-8].

