# gunzip — 解压 Gzip 文件

> **其他语言：** [English](../../en/applets/gunzip.md)

## 语法

```
gunzip [选项]... [文件]...
```

## 描述

`gunzip` 是与 `gzip -d` 共用流式引擎的专用解压入口。输出名称会移除 `.gz`，并将 `.tgz` 映射为 `.tar`。未指定文件或操作数为 `-` 时，从标准输入读取压缩数据并将明文写到标准输出。

## 选项

| 选项 | 描述 |
|------|------|
| `-k`, `--keep` | 保留压缩输入文件 |
| `-f`, `--force` | 覆盖已有输出文件 |
| `-c`, `--to-stdout` | 将解压数据写到标准输出 |

## 示例

```bash
idlebox gunzip archive.tar.gz
idlebox gunzip -k report.txt.gz
idlebox gunzip -c image.raw.gz > image.raw
```

[gzip](gzip.md) 中说明的失败安全输出与纯 Rust 后端保证同样适用于 `gunzip`。

## 终端行为

当标准输入为终端时，`gunzip` 会打印错误并退出，而不是阻塞等待输入。使用 `-f` 可强制解压，或从其他命令管道输入数据。

## 参见

- [gzip](gzip.md)
- [zcat](zcat.md)
