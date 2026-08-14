# cat — 连接文件并输出到标准输出

> **其他语言：** [English](../../en/applets/cat.md)

## 语法

```
cat [-n] [-b] [-A|-e] [文件...]
```

## 描述

`cat` Applet 按顺序读取文件并将其内容写入标准输出。如果未指定文件，或传入 `-`，则从标准输入（stdin）读取，支持管道用法。

## 选项

| 选项 | 描述 |
|------|------|
| `-n` | 为所有输出行编号 |
| `-b` | 仅为非空输出行编号（覆盖 `-n`） |
| `-A` | 等同于 `-vET`：显示不可打印字符、将 Tab 显示为 `^I`、在行末显示 `$` |
| `-e` | 等同于 `-vE`：显示不可打印字符、在行末显示 `$` |
| `--` | 选项结束标记；后续参数均视为文件路径 |

## 示例

```bash
# 输出文件内容
idlebox cat README.md

# 带行号输出
idlebox cat -n src/main.rs

# 仅非空行编号
idlebox cat -b src/main.rs

# 显示不可见字符
idlebox cat -A config.txt

# 从标准输入读取（管道）
echo "hello" | idlebox cat
# 输出: hello

# 连接多个文件
idlebox cat file1.txt file2.txt file3.txt
```

## 实现说明

- 位于 `src/applets/cat.rs`
- 使用 `BufReader` 实现高效缓冲 I/O
- 未指定文件或传入 `-` 时从 stdin 读取
- `-A` 标志将 Tab 显示为 `^I`，控制字符显示为 `^X`，并在每行末尾追加 `$`
- 行号使用右对齐的 6 字符宽度计数器，后跟 Tab 分隔符

## 参见

- [echo](echo.md) — 简单文本输出
- [ls](ls.md) — 列出目录内容
- [架构概览](../architecture.md)
