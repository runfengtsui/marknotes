---
Title: Android 平板安装 Linux 环境和虚拟桌面
Author: 邱彼郑楠
Date: 2025-07-15
Modified: 2025-07-16
---

# 初始化 Termux

首先, 使用 `pkg` 或 `apt` 更新软件包:

```bash
pkg update
pkg upgrade
```

启用 `x11` 和 `root` 仓库:

```bash
pkg install x11-repo root-repo
```

安装基础功能包:

```bash
pkg install termux-x11-nightly  # Termux-x11 软件通信
pkg install pulseaudio          # 声音支持
pkg install virglrenderer       # 在 Termux 启用 GPU 加速的 PRoot 容器
pkg install proot-distro        # PRoot 容器管理 Linux 发行版
```

申请存储权限:

```bash
termux-setup-storage
```

## 管理 Linux 发行版

使用 `proot-distro` 安装 Deepin (beige) 发行版:

```bash
proot-distro install deepin
```

进入 Deepin 容器中:

```bash
proot-distro login deepin
```

## 软件源管理

在容器中, 首先编辑 `/etc/apt/sources.list` 文件更换软件源, 选择清华源[^tsinghuadeepin]:

```
# 官方源
# deb https://community-packages.deepin.com/beige/ beige main commercial community
# 清华源
deb https://mirrors.tuna.tsinghua.edu.cn/deepin/beige/ beige main commercial community
```

然后更新软件包:

```bash
apt update
apt dist-upgrade
```

## 用户管理

初始化容器默认为 `root` 用户, 先使用 `useradd` 命令添加新用户:

```bash
useradd -m user
```

其中 `-m` 选项为新增用户创建家目录[^useradd]. 然后设置用户密码:

```bash
passwd user
```

最后安装 `sudo`:

```bash
apt install sudo
```

编辑 `/etc/sudoers` 文件为新用户设置 `sudo` 权限:

```
user    ALL=(ALL:ALL) ALL
```

## 桌面环境

使用 `Xfce4` 桌面环境:

```bash
sudo apt install xfce4
```

# 语言
## 系统语言

便于编程, 设置系统语言为英文, 编辑 `/etc/default/locale` 文件[^language]:

```
LANG="en_US.UTF-8"
LANGUAGE="en_US:en"
```

## 英文目录

如果家目录 (`/home/user`) 下的文件夹为中文路径, 可以通过修改 `~/.config/user-dirs.dirs` 文件更改为英文路径[^homenglish]:

```
XDG_DESKTOP_DIR="$HOME/Desktop"
XDG_DOWNLOAD_DIR="$HOME/Download"
XDG_TEMPLATES_DIR="$HOME/Templates"
XDG_PUBLICSHARE_DIR="$HOME/Public"
XDG_DOCUMENTS_DIR="$HOME/Documents"
XDG_MUSIC_DIR="$HOME/Music"
XDG_PICTURES_DIR="$HOME/Pictures"
XDG_VIDEOS_DIR="$HOME/Videos"
```

然后重命名对应的文件夹即可.

## 中文字体
但显示中文需要安装中文字体, 这里安装文泉驿正黑, Google Noto 开源字体等中文字体:

```bash
sudo apt install fonts-wqy-zenhei fonts-noto-cjk
```

## 输入法
对中文的输入需要使用 `fcitx5` 输入法:

```bash
sudo apt install fcitx5 fcitx5-pinyin
```

编辑 `~/.profile` 配置环境变量启用输入法:

```
export XMODIFIERS=@im=fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
```

## 时区

时区配置文件为 `/etc/localtime`, 所有时区配置文件在 `/usr/share/zoneinfo` 中[^zoneinfo], 设置时区为上海:

```bash
sudo ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

# 常用软件

火狐浏览器:

```bash
sudo apt install firefox
```

[^tsinghuadeepin]: 寻找繁星. Deepin使用笔记. 博客园: 2024.11.29[2025.07.15]. https://www.cnblogs.com/searchstar/p/18577813.
[^useradd]: 人在旅途QvQ. Linux系统使用添加新用户后，没有用户目录（没有home）解决办法. CSDN: 2020.05.12[2025.07.15]. https://blog.csdn.net/u013053075/article/details/106070566.
[^zoneinfo]: Alain. 使用Termux安装xfce4桌面,Android Studio, Code Server(VSCOode). Alain's Blog: 2023.10.19[2025.07.15]. https://www.alainlam.cn/?p=859.
[^language]: gfdgd xi. 命令更换deepin语言. CSDN: 2020.08.15[2025.07.15]. https://blog.csdn.net/weixin_46403483/article/details/107806010.
[^homenglish]: Teot. 修改Home下的目录为英文. 博客园: 2022.12.27[2025.07.16]. https://cnblogs.com/the-enjoyment-of-time/p/17008538.html.
