# cut — 从文件的每行中移除选定部分

> **其他语言：** [English](../../en/applets/cut.md)

## 语法

```
cut [选项]... [文件]...
```

## 描述

`cut` Applet 将每个文件中每行的选定部分输出到标准输出。可以按字符分隔的字段（列）选择，也可以按字符位置选择。不指定文件或文件为 `-` 时，从标准输入读取。

## 选项

| 选项 | 描述 |
|------|------|
| `-d`, `--delimiter=DELIM` | 使用 DELIM 作为字段分隔符（默认：TAB） |
| `-f`, `--fields=LIST` | 选择指定字段（如 `1`、`1,3`、`1-3`） |
| `-c`, `--characters=LIST` | 选择指定字符（如 `1-5`） |

字段/字符位置从 1 开始。范围如 `1-3` 选择位置 1 到 3。开放范围如 `3-` 选择从位置 3 到行尾。

## 退出状态

| 退出码 | 含义 |
|--------|------|
| 0 | 成功 |
| 1 | 发生错误 |

## 示例

```bash
# 提取 CSV 第一列
idlebox cut -d',' -f1 data.csv

# 提取第 1 和第 3 列
idlebox cut -d',' -f1,3 data.csv

# 提取字段范围
idlebox cut -d',' -f1-3 data.csv

# 提取第 1 到第 5 个字符
idlebox cut -c1-5 file.txt

# 从冒号分隔的 /etc/passwd 提取
idlebox cut -d: -f1 /etc/passwd

# 从 stdin 管道
echo "hello:world" | idlebox cut -d: -f2
# 输出: world

# 多个文件
idlebox cut -d',' -f1 file1.csv file2.csv
```

## 实现说明

- 位于 `src/applets/cut.rs`
- 默认分隔符为 TAB（匹配 POSIX 行为）
- 字段/字符位置从 1 开始（匹配 POSIX 惯例）
- 重叠范围按位置去重
- 支持开放范围（如 `3-`）

## 参见

- [sort](sort.md) — 排序文本行
- [grep](grep.md) — 基于模式的行选择
- [架构概览](../architecture.md)
