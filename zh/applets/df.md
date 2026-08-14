# df — 报告文件系统磁盘空间使用情况

> **其他语言：** [English](../../en/applets/df.md)

## 语法

```
df [-h] [FILE]
```

## 描述

`df` Applet 报告文件系统的磁盘空间使用情况。它从 `/proc/mounts` 读取挂载信息，并通过 `statvfs` 系统调用查询每个文件系统的空间数据。不带参数时显示所有已挂载的文件系统；指定路径时显示该路径所在文件系统的信息。

## 选项

| 选项 | 描述 |
|------|------|
| `-h`, `--human-readable` | 以人类可读格式显示容量（B, K, M, G, T） |

## 输出格式

```
Filesystem                 Size       Used      Avail  Use%  Mounted on
/dev/sda1                 50.0G      20.0G      30.0G   40%  /
```

## 示例

```bash
# 以人类可读格式显示所有文件系统
idlebox df -h

# 显示根目录所在文件系统的磁盘使用情况
idlebox df -h /

# 以原始块数显示 /tmp 的信息
idlebox df /tmp
```

## 实现说明

- 位于 `src/applets/df.rs`
- 解析 `/proc/mounts` 获取挂载点信息
- 通过 FFI 调用 POSIX `statvfs` 系统调用查询磁盘空间
- 列出所有挂载点时自动过滤伪文件系统（proc、sysfs、devtmpfs 等）
- 处理 `/proc/mounts` 中的八进制转义路径

## 参见

- [du](du.md) — 估算文件空间占用
- [架构概览](../architecture.md)
