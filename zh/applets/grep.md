# grep — 在文件或标准输入中搜索模式

> **其他语言：** [English](../../en/applets/grep.md)

## 语法

```
grep [选项]... 模式 [文件]...
```

## 描述

`grep` Applet 搜索匹配模式的行并输出。支持忽略大小写、反向匹配、显示行号、仅统计匹配数以及并行多线程搜索。不指定文件或文件为 `-` 时，从标准输入读取。

## 选项

| 选项 | 描述 |
|------|------|
| `-i`, `--ignore-case` | 模式匹配时忽略大小写 |
| `-v`, `--invert-match` | 反向匹配（只输出不匹配的行） |
| `-n`, `--line-number` | 在每行输出前添加 1-based 行号 |
| `-c`, `--count` | 仅输出每个文件的匹配行数统计 |
| `-j`, `--threads N` | 使用 N 个线程进行并行搜索（默认：自动检测 CPU 核心数） |

## 并行搜索引擎

`-j` / `--threads` 选项启用基于 Rust 标准库线程的并行多文件搜索。搜索多个文件时，工作负载会分配到多个工作线程，在多核系统上显著提升性能。

**核心特性：**
- 未指定 `-j` 时自动检测 CPU 核心数
- 有序结果收集机制保持 POSIX 兼容的输出顺序
- 标准输入或单文件搜索时自动回退到单线程模式
- 可通过 `-j N` 显式设置线程数（例如 `-j 4` 表示 4 个线程）

**性能优势：**
- 多文件搜索随可用 CPU 核心数线性扩展
- 大型目录树从并行 I/O 操作中获益
- 零外部依赖 - 纯 Rust 标准库实现

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

# 使用 4 个线程进行并行搜索
idlebox grep -j 4 "error" *.log

# 自动检测线程数的并行搜索
idlebox grep -j 0 "pattern" /var/log/*.log
```

## 实现说明

- 位于 `src/applets/grep.rs`
- 使用简单子串匹配（非正则表达式），不引入正则表达式或 Applet 专用 crate
- 忽略大小写模式对模式和行都进行小写转换后比较
- 匹配时返回退出码 0，无匹配返回 1，错误返回 2
- 多个文件时输出前添加 `文件名:`
- 行号为 1-based（遵循 POSIX 惯例）
- 未指定模式时，打印用法信息并以退出码 2 退出
- 并行引擎使用 `std::thread` 和 `std::sync` 原语（零外部依赖）
- 工作分发使用原子索引追踪实现最优负载均衡

## 参见

- [cat](cat.md) — 读取文件内容
- [head](head.md) — 读取文件开头部分
- [tail](tail.md) — 读取文件末尾部分
- [架构概览](../architecture.md)
