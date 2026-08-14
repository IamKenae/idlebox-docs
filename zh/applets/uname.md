# uname — 打印系统信息

> **其他语言：** [English](../../en/applets/uname.md)

## 语法

```
uname [OPTION]...
```

## 描述

`uname` Applet 通过 POSIX `uname()` 系统调用打印系统信息。不带任何选项时，打印内核名称（等同于 `-s`）。

## 选项

| 选项 | 描述 |
|------|------|
| `-a`, `--all` | 打印所有信息 |
| `-s`, `--sysname` | 打印内核名称（如 Linux） |
| `-n`, `--nodename` | 打印网络节点主机名 |
| `-r`, `--release` | 打印内核发行版（如 5.15.0-generic） |
| `-v`, `--version` | 打印内核版本 |
| `-m`, `--machine` | 打印机器硬件名称（如 x86_64） |

## 示例

```bash
# 打印内核名称（默认）
idlebox uname

# 打印所有系统信息
idlebox uname -a

# 打印内核发行版
idlebox uname -r

# 打印机器架构
idlebox uname -m

# 组合多个选项
idlebox uname -sm
```

## 输出格式

```
# uname -a
Linux myhost 5.15.0-generic #1 SMP Fri Jan 1 00:00:00 UTC 2024 x86_64
```

## 实现说明

- 位于 `src/applets/uname.rs`
- 通过 FFI 调用 POSIX `uname()` 系统调用
- 解析内核返回的 `utsname` 结构体
- 支持组合短选项（如 `-sm`、`-rn`）
- 字段按固定顺序打印：sysname、nodename、release、version、machine

## 参见

- [uptime](uptime.md) — 显示系统运行时间
- [架构概览](../architecture.md)
