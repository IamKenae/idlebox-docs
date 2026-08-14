# grep — 在文件或标准输入中搜索模式

> **其他语言：** [English](../../en/applets/grep.md)

## 语法

```
grep [选项]... 模式 [文件]...
```

## 描述

`grep` Applet 搜索匹配模式的行并输出。支持忽略大小写、反向匹配、显示行号和仅统计匹配数。不指定文件或文件为 `-` 时，从标准输入读取。

## 选项

| 选项 | 描述 |
|------|------|
| `-i`, `--ignore-case` | 模式匹配时忽略大小写 |
| `-v`, `--invert-match` | 反向匹配（只输出不匹配的行） |
| `-n`, `--line-number` | 在每行输出前添加 1-based 行号 |
| `-c`, `--count` | 仅输出每个文件的匹配行数统计 |

## 退出状态

| 退出码 | 含义 |
|--------|------|
| 0 | 至少找到一个匹配 |
| 1 | 没有匹配 |
| 2 | 发生错误 |

## 示例

```bash
# 基本模式搜索
idlebox grep "error" log.txt

# 忽略大小写搜索
idlebox grep -i "error" log.txt

# 显示行号
idlebox grep -n "TODO" source.rs

# 反向匹配（显示不匹配的行）
idlebox grep -v "debug" log.txt

# 统计匹配行数
idlebox grep -c "warning" log.txt

# 组合：忽略大小写 + 显示行号
idlebox grep -in "error" log.txt
# 输出: 3:Error occurred
#       7:ERROR: fatal
#       12:error: minor

# 从 stdin 管道搜索
cat log.txt | idlebox grep -i "error"

# 搜索多个文件
idlebox grep "pattern" file1.txt file2.txt
# 输出: file1.txt:matching line
#       file2.txt:another match
```

## 实现说明

- 位于 `src/applets/grep.rs`
- 使用简单子串匹配（非正则表达式），实现零依赖设计
- 忽略大小写模式对模式和行都进行小写转换后比较
- 匹配时返回退出码 0，无匹配返回 1，错误返回 2
- 多个文件时输出前添加 `文件名:`
- 行号为 1-based（遵循 POSIX 惯例）

## 参见

- [cat](cat.md) — 读取文件内容
- [head](head.md) — 读取文件开头部分
- [tail](tail.md) — 读取文件末尾部分
- [架构概览](../architecture.md)
