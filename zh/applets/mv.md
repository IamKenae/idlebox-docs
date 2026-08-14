# mv — 移动（重命名）文件与目录

> **其他语言：** [English](../../en/applets/mv.md)

## 语法

```
mv [选项]... 源文件... 目标
```

## 描述

`mv` Applet 用于移动或重命名文件与目录。当目标是一个已存在的目录时，源文件会被移入该目录。当只有一个源文件且目标不是目录时，源文件会被重命名。

## 行为

- 重命名文件和目录：`mv old.txt new.txt`
- 将多个项目移入目录：`mv f1 f2 target_dir/`
- 默认覆盖已存在的文件（不提示）
- **跨设备支持**：若 `rename()` 因 `EXDEV`（跨设备链接）失败，自动降级为复制 + 删除

## 示例

```bash
# 重命名文件
idlebox mv old_name.txt new_name.txt

# 将文件移入目录
idlebox mv file.txt target_dir/

# 将多个文件移入目录
idlebox mv file1.txt file2.txt file3.txt target_dir/

# 重命名目录
idlebox mv old_dir/ new_dir/

# 将目录移入另一个目录
idlebox mv mydir/ target_parent/
```

## 实现说明

- 位于 `src/applets/mv.rs`
- 优先使用 `std::fs::rename`（同一文件系统上的原子操作）
- 遇到 `EXDEV` 错误（跨设备）时，自动降级为递归复制 + 删除
- 跨设备降级同时支持文件和目录
- 当指定多个源时，最后一个参数被视为目标目录
- 若任一移动操作失败，返回退出码 1

## 参见

- [cp](cp.md) — 复制文件
- [rm](rm.md) — 删除文件
- [架构概览](../architecture.md)
