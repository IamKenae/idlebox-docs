# free — 显示内存使用情况

> **其他语言：** [English](../../en/applets/free.md)

## 语法

```
free [-h]
```

## 描述

`free` Applet 显示空闲和可用的物理内存及交换空间总量，以及内核使用的缓冲区与缓存。数据从 `/proc/meminfo` 读取。

## 选项

| 选项 | 描述 |
|------|------|
| `-h`, `--human-readable` | 以人类可读格式显示容量（B, K, M, G, T） |

## 输出格式

```
              total        used        free      shared   buff/cache   available
Mem:        8048564     4123456     1234567      234567     2690541     3654321
Swap:       2097148      123456     1973692
```

使用 `-h`：

```
              total        used        free      shared   buff/cache   available
Mem:           7.7G        3.9G        1.2G       229M        2.6G        3.5G
Swap:          2.0G       120.6M        1.9G
```

## 示例

```bash
# 以 KB 为单位显示内存使用情况
idlebox free

# 以人类可读格式显示内存使用情况
idlebox free -h
```

## 实现说明

- 位于 `src/applets/free.rs`
- 解析 `/proc/meminfo` 获取内存统计信息
- 读取字段：MemTotal、MemFree、MemAvailable、Shmem、Buffers、Cached、SwapTotal、SwapFree
- `/proc/meminfo` 中的值以千字节（kB）为单位
- 人类可读格式使用二进制单位（1K = 1024 字节）

## 参见

- [df](df.md) — 报告文件系统磁盘空间使用情况
- [架构概览](../architecture.md)
