---
Title: zathura 的编译安装与使用
Author: 邱彼郑楠
Date: 2024-04-01
Modified: 2024-06-13
---

在 Deepin V20.9 版本系统中可以直接使用包管理工具 `apt` 来安装 [zathura](https://git.pwmt.org/pwmt/zathura.git): `apt install zathura`. 然而 Deepin V23 Beta3 版本系统中的包管理工具 `apt` 是没有 `zathura` 这个软件的, 究其原因, 应该是包管理工具中缺乏 [girara](https://git.pwmt.org/pwmt/girara.git) 这个依赖项. 所以需要先编译安装依赖项, 再安装 `zathura`.

## girara

将源代码克隆到本地:

```git
git clone https://git.pwmt.org/pwmt/girara.git
```

安装依赖

```bash
# The following dependencies are required: libglib2.0-dev 系统已有
apt install libgtk-3-dev
# The following dependencies are optional: configuration dumpint support
apt install libjson-glib-dev
# For building, the following dependencies are also required:
apt install meson gettext pkgconf
# The following dependencies are optianal build-time only dependencies:
apt install check doxygen
```

编译过程比较简单

```bash
meson build
cd build
ninja
ninja install
```

在运行 `meson build` 命令之后, `xvfb-run` 这一项没有找到, 为避免之后出现问题, 也将这个装上去:

```bash
apt install xvfb
```

这样再运行 `ninja` 和 `ninja install` 命令就可以了.

## zathura

同样的步骤去编译 `zathura`:

```git
git clone https://git.pwmt.org/pwmt/zathura.git
```

安装依赖:

```bash
# The following dependencies are required: libgtk-3-dev libglib2.0-dev libjson-glib-dev 已安装 
apt install libmagic-dev libsqlite3-dev
# The following dependencies are optional:
apt install libsynctex-dev libseccomp-dev
# apt install meson gettext pkgconf
# The following dependencies are optional build-time only dependencies: check doxygen 已安装
apt install python3-sphinx
```

同样在运行 `meson build` 时候发现缺少了 `appstream-util`, 将其补充上去, `apt install appstream-util`, 再依次运行 `ninja` 和 `ninja install`.

现在, 输入 `zathura` 命令已经可以打开界面了. 尝试去打开文档, 会发现报了两个错误:

* 一个是无法识别文档类型;
* 一个是要求至少有一个插件;

也就是 `zathura` 实际上只是一个图形界面, 真正去渲染打开文档的是 [zathura-pdf-poppler](https://git.pwmt.org/pwmt/zathura-pdf-poppler.git) 这个插件. 当然也可以安装其他插件打开更多类型的文档.

## zathura-pdf-poppler

这个依赖比较少, 毕竟 `girara` 和 `zathura` 都已经安装好了, 只需要添加一个依赖即可:

```bash
apt install libpoppler-glib-dev
```

接下来 `meson build && cd build` 和 `ninja && ninja install` 一套流程成功安装.

再去打开文档, 成功打开!
