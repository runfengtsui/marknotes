---
Title: 软件疑难解答
Author: 邱彼郑楠
Date: 2022-11-05
Modified: 2022-11-30
---

# Windows 电脑
## 蓝牙无故消失

有可能是静电原因。关闭电脑，拔掉电源，静置一会解除静电即可。

# 阿里云服务器
## ssh 工具

通过 `ssh` 工具连接远程服务器时，如果一段时间没有使用，连接会自动中断，这非常不方便。可以单独为本次连接配置也可以在客户端进行配置，详细请参考 [解决ssh连接长时间不操作断开连接的问题（client_loop/ send disconnect/ Broken pipe）](https://zhuanlan.zhihu.com/p/431249844)。

1. 只让当前的 `ssh` 保持连接，可以使用以下命令：

```bash
ssh -o ServerAliveInterval=60 user@sshserver
```

2. 可以在客户端的 `~/.ssh/config` 配置文件中配置，不用每次输入 `-o ServerAliveInterval=60` 这一小段参数。在 `~/.ssh/config` 配置文件中添加以下内容：

```
# 针对所有的主机
Host *
    ServerAliveCountMax 5
    ServerAliveInterval 60
```
