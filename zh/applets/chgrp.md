# chgrp — 修改组所有权

> **其他语言：** [English](../../en/applets/chgrp.md)

## 语法

```
chgrp [-R] 组 文件...
```

## 描述

`chgrp` Applet 修改指定文件的组所有权。组可通过名称或数字 GID 指定。

## 选项

| 选项 | 描述 |
|------|------|
| `-R`, `--recursive` | 递归修改目录及其内部所有文件的组所有权 |

## 示例

```bash
# 将组改为 "users"
idlebox chgrp users file.txt

# 使用数字 GID 修改组
idlebox chgrp 1000 file.txt

# 递归修改目录的组所有权
idlebox chgrp -R users mydir/

# 修改多个文件的组
idlebox chgrp users file1.txt file2.txt
```

## 实现说明

- 位于 `src/applets/chgrp.rs`
- 使用 POSIX `chown()` 和 `lchown()` FFI 调用（UID 不变）
- 符号链接通过 `lchown()` 处理（不跟随符号链接）
- 零外部依赖 — 纯 Rust 标准库 + POSIX libc FFI

## 参见

- [chown](chown.md) — 修改文件所有者与组
- [chmod](chmod.md) — 修改文件权限位
- [ls](ls.md) — 查看文件所有权
- [架构概览](../architecture.md)
