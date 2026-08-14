# ln — 创建文件链接

> **其他语言：** [English](../../en/applets/ln.md)

## 语法

```
ln [OPTION]... TARGET LINK_NAME
ln [OPTION]... TARGET... DIRECTORY
```

## 描述

`ln` Applet 用于在文件之间创建链接。默认创建硬链接；使用 `-s` 选项则创建符号（软）链接。

硬链接是指向与原始文件相同 inode 的目录条目。符号链接是一种特殊文件，包含对另一个文件的路径引用。

## 选项

| 选项 | 描述 |
|------|------|
| `-s`, `--symbolic` | 创建符号链接而非硬链接 |
| `-f`, `--force` | 创建链接前删除已存在的目标文件 |

## 示例

```bash
# 创建符号链接
idlebox ln -s /path/to/target /path/to/link

# 创建硬链接
idlebox ln /path/to/target /path/to/link

# 强制覆盖已存在的链接
idlebox ln -sf /path/to/target /path/to/existing_link

# 将多个文件链接到目录中
idlebox ln -s file1.txt file2.txt /path/to/directory/
```

## 实现说明

- 位于 `src/applets/ln.rs`
- 使用 `std::os::unix::fs::symlink` 创建符号链接
- 使用 `std::fs::hard_link` 创建硬链接
- 支持组合短选项（如 `-sf`）
- 将多个文件链接到目录时，链接名取自源文件名

## 参见

- [readlink](readlink.md) — 打印已解析的符号链接
- [架构概览](../architecture.md)
