# wc — 打印每个文件的换行、单词和字节计数

> **其他语言：** [English](../../en/applets/wc.md)

## 语法

```
wc [选项]... [文件]...
```

## 描述

`wc` Applet 打印每个文件的换行数、单词数和字节数。不指定文件或文件为 `-` 时，从标准输入读取。当提供多个文件时，末尾会输出 `total` 汇总行。

## 选项

| 选项 | 描述 |
|------|------|
| `-l`, `--lines` | 打印换行计数 |
| `-w`, `--words` | 打印单词计数 |
| `-c`, `--bytes` | 打印字节计数 |
| `-m`, `--chars` | 打印字符计数 |

不指定选项时，`wc` 默认打印行数、单词数和字节数。

## 退出状态

| 退出码 | 含义 |
|--------|------|
| 0 | 成功 |
| 1 | 发生错误 |

## 示例

```bash
# 统计文件行数
idlebox wc -l file.txt

# 统计文件单词数
idlebox wc -w file.txt

# 统计文件字节数
idlebox wc -c file.txt

# 默认：行数、单词数、字节数
idlebox wc file.txt

# 从 stdin 管道统计
cat file.txt | idlebox wc -l

# 多个文件（显示总计）
idlebox wc -l file1.txt file2.txt
# 输出:
#       3 file1.txt
#       5 file2.txt
#       8 total
```

## 实现说明

- 位于 `src/applets/wc.rs`
- 使用固定 8 KiB 缓冲区流式读取，不再缓存整个文件
- 只请求字节数和/或换行数时跳过 Unicode 解码
- 跨 UTF-8 缓冲区边界保持正确的字符与 Unicode 空白单词计数；无效序列沿用有损替换语义
- 多个文件时输出 `total` 汇总行
- 输出右对齐，每列宽度为 7 个字符

## 参见

- [cat](cat.md) — 读取文件内容
- [sort](sort.md) — 排序文本行
- [架构概览](../architecture.md)
