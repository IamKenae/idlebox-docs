# cp — 复制文件与目录

> **其他语言：** [English](../../en/applets/cp.md)

## 语法

```
cp [选项]... 源文件... 目标
```

## 描述

`cp` Applet 用于复制文件和目录。复制单个文件到目标位置会创建或覆盖目标文件。复制多个源文件或目录时，目标必须是一个目录。

## 选项

| 选项 | 描述 |
|------|------|
| `-r`, `-R`, `--recursive` | 递归复制目录 |
| `-f`, `--force` | 强制覆盖已存在的目标文件 |

选项可组合使用：`-rf`、`-fr` 等。

## 示例

```bash
# 复制单个文件
idlebox cp source.txt dest.txt

# 将文件复制到目录中
idlebox cp file.txt target_dir/

# 将多个文件复制到目录中
idlebox cp file1.txt file2.txt file3.txt target_dir/

# 递归复制目录
idlebox cp -r src_dir/ dst_dir/

# 强制覆盖
idlebox cp -f source.txt dest.txt

# 递归复制并强制覆盖
idlebox cp -rf project/ backup/
```

## 实现说明

- 位于 `src/applets/cp.rs`
- 文件复制使用 `std::fs::copy`（保留内容，不保留元数据）
- 递归目录复制会遍历整个目录树并重建完整结构
- 不使用 `-r` 时，尝试复制目录会报错并跳过
- 当指定多个源时，最后一个参数被视为目标目录
- 若任一复制操作失败，返回退出码 1

## 参见

- [mv](mv.md) — 移动文件
- [rm](rm.md) — 删除文件
- [架构概览](../architecture.md)
