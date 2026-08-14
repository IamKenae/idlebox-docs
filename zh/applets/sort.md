# sort — 排序文本文件的行

> **其他语言：** [English](../../en/applets/sort.md)

## 语法

```
sort [选项]... [文件]...
```

## 描述

`sort` Applet 将所有文件的排序合并结果写入标准输出。不指定文件或文件为 `-` 时，从标准输入读取。多个文件会合并后一起排序。

## 选项

| 选项 | 描述 |
|------|------|
| `-r`, `--reverse` | 反转比较结果（降序排列） |
| `-n`, `--numeric-sort` | 按字符串数值大小排序 |
| `-u`, `--unique` | 仅输出唯一行（去重） |

## 退出状态

| 退出码 | 含义 |
|--------|------|
| 0 | 成功 |
| 1 | 发生错误 |

## 示例

```bash
# 基本字母排序
idlebox sort file.txt

# 数值排序
idlebox sort -n numbers.txt

# 反转（降序）排序
idlebox sort -r file.txt

# 数值降序排序
idlebox sort -n -r numbers.txt

# 排序并去重
idlebox sort -u file.txt

# 从 stdin 管道排序
cat file.txt | idlebox sort

# 合并排序多个文件
idlebox sort file1.txt file2.txt
```

## 实现说明

- 位于 `src/applets/sort.rs`
- 数值排序将每行解析为 f64；非数值行按 0 处理
- 去重模式在排序后使用 `dedup()`（移除相邻重复项）
- 多个文件读入单一缓冲区后统一排序
- 默认排序为字典序（字节比较）

## 参见

- [uniq](uniq.md) — 过滤重复行
- [wc](wc.md) — 统计行数
- [架构概览](../architecture.md)
