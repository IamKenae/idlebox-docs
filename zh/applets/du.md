# du — 估算文件空间占用

> **其他语言：** [English](../../en/applets/du.md)

## 语法

```
du [-h] [-s] [-d N] [FILE]...
```

## 描述

`du` Applet 通过递归累加每个条目所占用的磁盘块来估算文件与目录的空间占用。大小基于实际磁盘块使用量（通过 `MetadataExt::blocks` 获取），而非逻辑文件大小。

## 选项

| 选项 | 描述 |
|------|------|
| `-h`, `--human-readable` | 以人类可读格式显示体积（B, K, M, G, T） |
| `-s`, `--summarize` | 仅显示每个参数的总体积 |
| `-d N`, `--max-depth N` | 仅在目录深度不超过 N 层时输出总计 |

## 示例

```bash
# 显示当前目录的磁盘占用
idlebox du

# 仅显示 /var/log 的总占用
idlebox du -s /var/log

# 人类可读格式，最大深度 1 层
idlebox du -h -d 1 /home

# 人类可读的汇总
idlebox du -h -s /tmp
```

## 实现说明

- 位于 `src/applets/du.rs`
- 使用 `std::os::unix::fs::MetadataExt::blocks()` 获取实际磁盘块占用
- 块大小按 `blocks * 512` 字节计算（POSIX 标准）
- 未指定路径时默认为当前目录
- `-d 0` 等价于 `-s`

## 参见

- [df](df.md) — 报告文件系统磁盘空间使用情况
- [ls](ls.md) — 列出目录内容及大小
- [架构概览](../architecture.md)
