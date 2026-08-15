# zcat — 将 Gzip 数据解压到标准输出

> **其他语言：** [English](../../en/applets/zcat.md)

## 语法

```
zcat [文件]...
```

## 描述

`zcat` 将每个指定的 Gzip 文件解压到标准输出，不修改或删除源文件。未指定文件或操作数为 `-` 时，从标准输入读取 Gzip 流。其用途等同于常见的 `gzip -dc` 工作流。

## 示例

```bash
idlebox zcat server.log.gz
idlebox zcat part-1.gz part-2.gz > combined.txt
idlebox cat payload.gz | idlebox zcat
```

## 终端行为

当标准输入为终端时，`zcat` 会打印错误并退出，而不是阻塞等待输入。使用管道从其他命令输入数据即可从标准输入解压。

## 参见

- [gzip](gzip.md)
- [gunzip](gunzip.md)
- [cat](cat.md)
