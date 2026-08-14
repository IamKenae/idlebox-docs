# mkdir — 创建目录

> **其他语言：** [English](../../en/applets/mkdir.md)

## 语法

```
mkdir [选项]... 目录...
```

## 描述

`mkdir` Applet 用于创建一个或多个目录。默认情况下，父目录必须已存在。使用 `-p` 可按需自动创建中间目录。

## 选项

| 选项 | 描述 |
|------|------|
| `-p`, `--parents` | 按需创建父目录；若目录已存在则不报错 |

## 示例

```bash
# 创建单个目录
idlebox mkdir mydir

# 创建嵌套目录（父目录不存在时会失败）
idlebox mkdir a/b/c
# 错误: No such file or directory

# 使用 -p 创建嵌套目录
idlebox mkdir -p a/b/c

# 一次创建多个目录
idlebox mkdir dir1 dir2 dir3

# 组合用法：创建多个嵌套路径
idlebox mkdir -p project/src project/tests project/docs/api
```

## 实现说明

- 位于 `src/applets/mkdir.rs`
- 默认使用 `std::fs::create_dir`，带 `-p` 时使用 `std::fs::create_dir_all`
- 多个目录按顺序处理，某个目录创建失败不影响其他目录
- 若任一目录创建失败，返回退出码 1

## 参见

- [rm](rm.md) — 删除目录
- [架构概览](../architecture.md)
