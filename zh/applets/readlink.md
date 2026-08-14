# readlink — 打印已解析的符号链接或规范文件名

> **其他语言：** [English](../../en/applets/readlink.md)

## 语法

```
readlink [OPTION]... FILE...
```

## 描述

`readlink` Applet 打印符号链接的目标。使用 `-f` 选项时，递归解析路径中的所有符号链接，输出规范的绝对路径。

## 选项

| 选项 | 描述 |
|------|------|
| `-f`, `-e`, `--canonicalize` | 跟踪每个组件中的每个符号链接进行规范化，解析为绝对路径 |
| `-n`, `--no-newline` | 不输出末尾的换行符 |

## 示例

```bash
# 读取符号链接的目标
idlebox readlink /path/to/symlink

# 解析为规范的绝对路径
idlebox readlink -f /path/to/symlink

# 读取时不带末尾换行符
idlebox readlink -n /path/to/symlink

# 组合选项
idlebox readlink -fn /path/to/symlink
```

## 输出

不带 `-f` 时，打印直接的符号链接目标（可能是相对路径）。
带 `-f` 时，打印完全解析的绝对路径，所有符号链接均已展开。

## 实现说明

- 位于 `src/applets/readlink.rs`
- 使用 `std::fs::read_link` 读取符号链接目标
- 使用 `std::fs::canonicalize` 进行完整路径解析
- 支持组合短选项（如 `-fn`、`-ne`）
- 可在单次调用中处理多个文件

## 参见

- [ln](ln.md) — 创建文件链接
- [架构概览](../architecture.md)
