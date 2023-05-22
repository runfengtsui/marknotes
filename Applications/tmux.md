---
Title: tmux 使用教程
Author: 邱彼郑楠
Date: 2023-05-15
Modified: 2023-05-20
---

# 外部命令[^key]
[^key]: [Tmux的常用快捷键](https://zhuanlan.zhihu.com/p/137715607).
## 会话
### 新建会话

创建一个指定名称的会话使用命令 `tmux new -s <session-name>`.

### 查看已有会话

使用 `tmux ls` 命令查看当前已有的所有会话.

### 接入会话

如果想要接入其中某一个会话, 需要使用 `tmux attach -t <session-name>` 命令.

### 退出会话

相对于接入会话, 退出当前会话使用 `tmux detach` 命令. 退出后仍可通过 `attach` 接入会话.

### 杀死会话

当某个会话不在使用, 可以通过 `tmux kill-session -t <session-name>` 杀死某一个会话, 该会话不能再被接入.

### 切换会话

在不同的会话中切换, 可以使用 `tmux switchc -t <session-name>` 命令.

### 重命名会话

对其中某一个会话重命名, 需要使用 `tmux rename -t <session-name> <new-session-name>` 命令.

## 窗口
### 上下拆分

将窗口拆分为上下两个窗格, 使用命令 `tmux split-window` 即可.

### 左右拆分

将窗口拆分为左右两个窗格, 在上下拆分窗口命令的基础上, 增加 `-h` 参数, 即 `tmux split-window -h`.

如果需要在左右拆分和上下拆分之间调整, 可以使用

### 窗口跳转

窗口拆分之后, 如果需要在不同窗口之间移动, 可以使用 `Ctrl+b` 加上方向键. 值得注意的是, 按下 `Ctrl+b` 松开再按方向键是窗口跳转; 而按下 `Ctrl+b` 的同时按方向键是调整窗格的大小.

# 其他设置
## 鼠标支持

tmux 默认是不支持鼠标操作的, 可以通过 `tmux set mouse on` 命令设定鼠标滚动支持[^mouse].
[^mouse]: [tmux使用指南：5 :滚动与鼠标支持](https://blog.csdn.net/liumiaocn/article/details/104100000)

# 配置

Tmux 的用户配置文件为 `~/.tmux.conf`, 在修改了 `.tmux.conf` 文件之后, 需要重启 Tmux 才能生效, 即使用 `restart tmux` 命令; 或者在 Tmux 窗口中, 按下 `prefix` 键, 再按下 `:` 键输入以下命令:

```
source-file ~/.tmux.conf
```

详细的配置见 [配置文件]().

配置参考 [Tmux配置](https://cloud.tencent.com/developer/article/2173566).
