---
Title: Linux 脚本编程
Author: 邱彼郑楠
Date: 2023-07-15
Modified: 2024-03-26
---

# 解压缩文件

* 对于 `*.tar.gz` 文件, 使用 `tar -zxvf` 命令解压;
* 对于 `*.tar.xz` 文件, 使用 `tar -xf` 命令解压;
* 对于 `*.tar.bz2` 文件, 使用 `tar -jxf` 命令解压;

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

