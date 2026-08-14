# su — 切换用户

> **其他语言：** [English](../../en/applets/su.md)

## 语法

```
su [选项] [用户]
```

## 描述

`su` Applet 允许以替代用户和组 ID 运行 Shell。若未指定用户，默认切换到 `root`。**注意：仅 root 可以切换到其他用户。**

## 选项

| 选项 | 描述 |
|------|------|
| `-`, `-l`, `--login` | 模拟登录 Shell（重置环境变量） |
| `-c`, `--command` | 切换身份后执行单条命令 |
| `-s`, `--shell` | 指定使用的 Shell |

## 示例

```bash
# 切换到 root（需要 root 权限）
idlebox su

# 切换到指定用户
idlebox su 用户名

# 以其他用户身份执行单条命令
idlebox su -c "whoami" root

# 模拟登录 Shell
idlebox su -l 用户名

# 使用指定的 Shell
idlebox su -s /bin/bash 用户名
```

## 实现说明

- 位于 `src/applets/su.rs`
- 使用 POSIX `getpwnam()` 和 `getuid()` FFI 调用
- 登录 Shell 模式会重置 `HOME`、`USER`、`SHELL`、`LOGNAME` 和 `PATH` 环境变量
- 仅 root（UID 0）可以切换到其他用户；非 root 用户将收到权限拒绝错误
- 零外部依赖 — 纯 Rust 标准库 + POSIX libc FFI

## 参见

- [id](id.md) — 打印用户与组 ID
- [whoami](whoami.md) — 打印有效用户名
- [架构概览](../architecture.md)
