---
Title: Linux
Author: 邱彼郑楠
Date: 2023-07-15
Modified: 2025-10-18
---

# 解压缩文件
## `Tar` 归档[^tar]

* 对于 `*.tar.gz` 和 `*.tgz` 类型文件, 使用的是 `gzip` 进行压缩, 需要使用 `tar xzvf` 命令解压;
* 对于 `*.tar.xz` 文件, 使用的是 `xz` 进行压缩, 需要使用 `tar xJvf` 命令解压;
* 对于 `*.tar.bz2` 文件, 使用的是 `bzip2` 进行压缩, 需要使用 `tar xjvf` 命令解压;
其中参数 `x` 表示解压, `c` 表示建立新的归档文件;
对于压缩/解压方式, `z` 表示调用 `gzip` 工具, `J` 表示调用 `xz` 工具, `j` 表示调用 `bzip2` 工具;
对于其他参数, `v` 表示在操作过程中显示详细信息, `f` 后面跟归档文件名称.

# 磁盘格式化分区

对于 GPT 分区表, 使用 `parted` 对磁盘进行分区, 支持超过 2 TB 的磁盘.
以磁盘 /dev/sda 为例, 开始分区:

```bash
sudo parted /dev/sda
```

修改磁盘格式为 GPT:

```bash
(parted) mklabel gpt
```

使用 `mkpart` 命令创建主分区 (GPT 支持更多的主分区), 其语法如下[^mkpart]:

```bash
(parted) mkpart primary <type> <start> <end>
```
其中 `<type>` 为文件系统类型, 不会实际格式化分区, 可不写;
`<start>` 为新分区的起始位置, 可以使用单位或者百分比表示;
`<end>` 为新分区的结束位置, 使用全部剩余空间标志为 `-1` 或 `100%`.

创建一个起始位置为 1 Mib, 结束位置为磁盘的大小一半的主分区:

```bash
(parted) mkpart primary 1Mib 50%
```

提示警告创建的该分区没有对齐以实现最佳性能. 需要手动获取对其参数[^alignment]:

```bash
cat /sys/block/sda/queue/optimal_io_size
cat /sys/block/sda/queue/minimum_io_size
cat /sys/block/sda/alignment_offset
cat /sys/block/sda/queue/physical_block_size
```

计算得到起始扇区为

```python
(optimal_io_size + alignment_offset) / physical_block_size
```

创建分区完成后, 使用 `quit/q` 命令退出. 然后使用 `mkfs` 命令格式化新分区:

```bash
# sudo mkfs.ext4 /dev/sda1
sudo mkfs -t ext4 /dev/sda1
# sudo mkfs -t ntfs /dev/sda1
```

另外, 可以使用 `tune2fs` 命令修改 `ext2`, `ext3` 和 `ext4` 文件系统的卷标.
在保证目标分区没有被使用的情况下 (首先卸载目标分区), 修改命令如下:

```bash
sudo tune2fs /dev/sda1 -L newname
```

如果是 `NTFS` 文件系统, 可以使用 `ntfslabel` 命令修改:

```bash
sudo ntfslabel /dev/sda1 newname
```

修改后重新挂载即可.

如果出现无法读写问题, 使用 `chmod 777` 更改权限即可.

# 空设备文件 `/dev/null`

所有追加到 `/dev/null` 文件的内容都将被清空, 所以可以用来隐藏标准输出和标准错误输出. 具体方式如下[^devnull]:

* `> /dev/null`: 可以输出标准错误输出, 忽略标准输出;
* `2> /dev/null`: 可以输出标准输出, 忽略标准错误输出;
* `> /dev/null 2>&1`: 同时忽略标准输出和标准错误输出;

另外, 如果想要清空文件内容但不删除文件, 可以考虑使用如下方式:

```bash
cat <filename> > /dev/null
```

[^tar]: itas109. [linux下使用 tar 来压缩和解压 tar.gz 和 tar.xz 文件](https://blog.csdn.net/itas109/article/details/136853283)[OL]. CSDN: 2024-03-19[2025-09-26]. https://blog.csdn.net/itas109/article/details/136853283.
[^mkpart]: GaGa. [parted mkpart命令创建分区](https://blog.mvpbang.com/p/50654760a598452e92489a43ac3a1e5a/)[OL]. GaGa's Blog: 2025-07-05[2025-10-18]. https://blog.mvpbang.com/p/50654760a598452e92489a43ac3a1e5a/.
[^alignment]: 苏浩智. [使用partedmklk对齐分区，以获得最佳性能](https://blog.51cto.com/suhaozhi/1754627)[OL]. 51CTO: 2016-03-24[2025-10-18]. https://blog.51cto.com/suhaozhi/1754627.
[^devnull]: Hxxx. [关于/dev/null](https://zhuanlan.zhihu.com/p/498303331)[OL]. 知乎: 2022-04-14[2023-07-15]. https://zhuanlan.zhihu.com/p/498303331.

