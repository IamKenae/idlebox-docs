# find — 搜索文件

> **其他语言：** [English](../../en/applets/find.md)

## 语法

```
find [PATH...] [OPTIONS]
```

## 描述

`find` Applet 递归搜索目录层次结构，查找匹配指定条件的文件。如果未指定路径，默认使用当前目录（`.`）。

## 选项

| 选项 | 描述 |
|------|------|
| `-name PATTERN` | 使用通配符模式匹配文件名（如 `*.rs`、`test_??.txt`） |
| `-type TYPE` | 按类型筛选：`f`（普通文件）、`d`（目录）、`l`（符号链接） |
| `-maxdepth N` | 限制递归深度（0 = 仅起始路径本身） |
| `-empty` | 仅匹配空文件或空目录 |

## 通配符语法

`-name` 选项支持简单的通配符模式：
- `*` 匹配任意字符序列
- `?` 匹配任意单个字符
- 其他字符按字面匹配

## 示例

```bash
# 查找所有 Rust 源文件
idlebox find . -name "*.rs"

# 查找所有目录
idlebox find /tmp -type d

# 限制深度查找文件
idlebox find . -name "*.txt" -maxdepth 2

# 查找空文件和空目录
idlebox find . -empty

# 组合选项
idlebox find . -type f -name "*.log" -empty

# 查找符号链接
idlebox find /usr -type l
```

## 实现说明

- 位于 `src/applets/find.rs`
- 使用 `std::fs::read_dir` 进行目录遍历
- 通配符匹配使用简单的状态机实现（无外部正则库）
- 结果在每个目录层级内按字母顺序排序
- 使用 `symlink_metadata` 正确识别符号链接而不跟踪它们
- 仅使用 Rust 标准库

## 参见

- [ls](ls.md) — 列出目录内容
- [test](test.md) — 文件测试运算符
- [架构概览](../architecture.md)
