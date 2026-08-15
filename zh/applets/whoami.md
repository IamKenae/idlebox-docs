# whoami — 打印有效用户名

> **其他语言：** [English](../../en/applets/whoami.md)

## 语法

```
whoami
```

## 描述

`whoami` Applet 打印当前有效用户的用户名。等价于 `id -un`。

## 选项

无。

## 示例

```bash
# 打印当前有效用户名
idlebox whoami
```

## 实现说明

- 位于 `src/applets/whoami.rs`
- 使用 POSIX `geteuid()` 和 `getpwuid()` FFI 调用
- 无 Applet 专属 crate 依赖 — Rust 标准库 + POSIX libc FFI

## 参见

- [id](id.md) — 打印真实与有效用户及组 ID
- [架构概览](../architecture.md)
