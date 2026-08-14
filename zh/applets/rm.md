# rm — 删除文件或目录

> **其他语言：** [English](../../en/applets/rm.md)

## 语法

```
rm [选项]... 文件...
```

## 描述

`rm` Applet 用于删除文件，配合 `-r` 可递归删除目录及其内容。不使用 `-r` 时，无法删除目录。

## 选项

| 选项 | 描述 |
|------|------|
| `-r`, `-R`, `--recursive` | 递归删除目录及其内容 |
| `-f`, `--force` | 忽略不存在的文件，不提示确认 |

选项可组合使用：`-rf`、`-fr`、`-Rf` 或分别指定 `-r -f`。

## 示例

```bash
# 删除单个文件
idlebox rm file.txt

# 删除多个文件
idlebox rm file1.txt file2.txt file3.txt

# 删除目录及其所有内容
idlebox rm -r mydir

# 强制删除，不存在的文件不报错
idlebox rm -f nonexistent.txt

# 递归强制删除（常见的清理模式）
idlebox rm -rf build/ dist/

# 不使用 -r 删除目录会失败
idlebox rm mydir
# 错误: Is a directory
```

## 实现说明

- 位于 `src/applets/rm.rs`
- 文件使用 `std::fs::remove_file`，目录使用 `std::fs::remove_dir_all`
- 不使用 `-r` 时，尝试删除目录会报错并返回退出码 1
- 使用 `-f` 时，不存在的路径会被静默跳过
- 支持组合短选项（如 `-rf`）

## 参见

- [mkdir](mkdir.md) — 创建目录
- [cp](cp.md) — 复制文件
- [架构概览](../architecture.md)
