---
Title: Linux 脚本编程
Author: 邱彼郑楠
Date: 2023-07-15
Modified: 2025-09-26
---

# 解压缩文件
## `Tar` 归档[^tar]

* 对于 `*.tar.gz` 和 `*.tgz` 类型文件, 使用的是 `gzip` 进行压缩, 需要使用 `tar xzvf` 命令解压;
* 对于 `*.tar.xz` 文件, 使用的是 `xz` 进行压缩, 需要使用 `tar xJvf` 命令解压;
* 对于 `*.tar.bz2` 文件, 使用的是 `bzip2` 进行压缩, 需要使用 `tar xjvf` 命令解压;
其中参数 `x` 表示解压, `c` 表示建立新的归档文件;
对于压缩/解压方式, `z` 表示调用 `gzip` 工具, `J` 表示调用 `xz` 工具, `j` 表示调用 `bzip2` 工具;
对于其他参数, `v` 表示在操作过程中显示详细信息, `f` 后面跟归档文件名称.

# 空设备文件 `/dev/null`

所有追加到 `/dev/null` 文件的内容都将被清空, 所以可以用来隐藏标准输出和标准错误输出. 具体方式如下[^devnull]:

* `> /dev/null`: 可以输出标准错误输出, 忽略标准输出;
* `2> /dev/null`: 可以输出标准输出, 忽略标准错误输出;
* `> /dev/null 2>&1`: 同时忽略标准输出和标准错误输出;

另外, 如果想要清空文件内容但不删除文件, 可以考虑使用如下方式:

```bash
cat <filename> > /dev/null
```

[^devnull]: Hxxx.[关于/dev/null](https://zhuanlan.zhihu.com/p/498303331)[OL].(2022-04-14)[2023-07-15].
[^tar]: itas109. [linux下使用 tar 来压缩和解压 tar.gz 和 tar.xz 文件](https://blog.csdn.net/itas109/article/details/136853283).(2024-03-19)[2025-09-26].

