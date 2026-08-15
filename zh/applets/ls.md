# ls — 列出目录内容

> **其他语言：** [English](../../en/applets/ls.md)

## 语法

```
ls [-a] [-l] [-h] [--color[=何时]] [路径...]
```

## 描述

`ls` Applet 列出目录的内容。它是 IdleBox 中功能最丰富的 Applet 之一，完整支持 ANSI 彩色输出，让终端导航成为一种视觉享受。

## 选项

| 选项 | 描述 |
|------|------|
| `-a`, `--all` | 显示所有条目，包括隐藏文件（以 `.` 开头的文件） |
| `-l` | 使用长格式列表（权限、所有者、大小、日期） |
| `-h`, `--human-readable` | 配合 `-l`，以人类可读格式显示大小（如 `1.2K`、`3.4M`） |
| `--color` | 彩色输出（等同于 `--color=always`） |
| `--color=auto` | 仅在输出到终端（TTY）时彩色显示 |
| `--color=always` | 始终彩色输出 |
| `--color=never` | 始终不彩色输出 |

选项可以短格式组合使用：`-la`、`-lh`、`-lah` 等。

## 配色方案

启用颜色后，`ls` 使用以下 ANSI 配色方案：

| 类型 | 颜色 | 代码 |
|------|------|------|
| 目录 | **粗体蓝色** | `1;34` |
| 符号链接 | **粗体青色** | `1;36` |
| 可执行文件 | **粗体绿色** | `1;32` |
| 压缩包（`.tar`、`.gz`、`.zip` 等） | **粗体红色** | `1;31` |
| 普通文件 | 默认 | — |

## 示例

```bash
# 基本列表
idlebox ls

# 显示隐藏文件
idlebox ls -a

# 长格式
idlebox ls -l

# 长格式 + 人类可读大小
idlebox ls -lh

# 彩色输出
idlebox ls --color=auto

# 所有选项组合
idlebox ls -lah --color=auto

# 列出指定路径
idlebox ls /usr/bin /usr/local/bin
```

## 长格式输出

`-l` 标志产生以下格式的输出：

```
-rw-r--r--   1  1000  1000     1234 Aug 15 10:30 README.md
drwxr-xr-x   3  1000  1000     4096 Aug 14 09:00 src
-rwxr-xr-x   1  1000  1000   616736 Aug 15 01:55 idlebox
```

字段：`类型+权限`、`链接数`、`UID`、`GID`、`大小`、`修改日期`、`文件名`

## 实现说明

- 位于 `src/applets/ls.rs`
- TTY 检测使用 Rust 标准库 `IsTerminal` API 自动判断是否支持颜色
- 人类可读大小使用二进制单位（1K = 1024 字节）
- 时间戳使用自定义日期计算格式化（无 chrono 依赖）
- 权限位包含 SUID/SGID/sticky 位指示符（`s`、`S`、`t`、`T`）
- 条目按文件名字母顺序排序

## 参见

- [cat](cat.md) — 读取文件内容
- [架构概览](../architecture.md)
