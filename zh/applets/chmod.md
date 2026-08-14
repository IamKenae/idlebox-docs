# chmod — 修改文件权限位

> **其他语言：** [English](../../en/applets/chmod.md)

## 语法

```
chmod [-R] MODE FILE...
```

## 描述

`chmod` Applet 用于修改指定文件或目录的权限位。支持八进制数字模式（如 `755`、`0644`）。

## 选项

| 选项 | 描述 |
|------|------|
| `-R`, `--recursive` | 递归修改目录及其内部所有文件的权限 |

## 示例

```bash
# 设置文件权限为 755 (rwxr-xr-x)
idlebox chmod 755 script.sh

# 设置多个文件权限为 0644 (rw-r--r--)
idlebox chmod 0644 file1.txt file2.txt

# 递归修改目录权限
idlebox chmod -R 755 mydir/
```

## 实现说明

- 位于 `src/applets/chmod.rs`
- 使用 Rust 标准库的 `std::os::unix::fs::PermissionsExt`
- 模式参数以八进制（base 8）解析
- 递归模式会遍历目录中的所有条目

## 参见

- [ls](ls.md) — 查看文件权限
- [架构概览](../architecture.md)
