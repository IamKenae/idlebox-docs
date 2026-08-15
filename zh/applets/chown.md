# chown — 修改文件所有者与组

> **其他语言：** [English](../../en/applets/chown.md)

## 语法

```
chown [-R] [所有者][:[组]] 文件...
```

## 描述

`chown` Applet 修改指定文件的用户和/或组所有权。所有者和组可通过名称或数字 ID 指定。

## 选项

| 选项 | 描述 |
|------|------|
| `-R`, `--recursive` | 递归修改目录及其内部所有文件的所有者 |

## 所有者/组语法

| 语法 | 描述 |
|------|------|
| `user` | 将所有者改为 `user`，保持当前组 |
| `user:group` | 将所有者改为 `user`，组改为 `group` |
| `:group` | 保持当前所有者，将组改为 `group` |
| `user:` | 将所有者改为 `user`，组设为用户的登录组 |
| `1000:1000` | 使用数字 UID 和 GID |

## 示例

```bash
# 将文件所有者改为 root
idlebox chown root file.txt

# 同时修改所有者和组
idlebox chown user:group file.txt

# 仅修改组
idlebox chown :group file.txt

# 递归修改目录的所有权
idlebox chown -R user:group mydir/

# 使用数字 ID
idlebox chown 1000:1000 file.txt
```

## 实现说明

- 位于 `src/applets/chown.rs`
- 使用 POSIX `chown()` 和 `lchown()` FFI 调用
- 符号链接通过 `lchown()` 处理（不跟随符号链接）
- 无 Applet 专属 crate 依赖 — Rust 标准库 + POSIX libc FFI

## 参见

- [chgrp](chgrp.md) — 修改组所有权
- [chmod](chmod.md) — 修改文件权限位
- [ls](ls.md) — 查看文件所有权
- [架构概览](../architecture.md)
