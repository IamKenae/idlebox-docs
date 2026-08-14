# echo — 输出文本到标准输出

> **其他语言：** [English](../../en/applets/echo.md)

## 语法

```
echo [-n] [字符串...]
```

## 描述

`echo` Applet 将其参数写入标准输出，参数之间以空格分隔，末尾附加换行符。它是 IdleBox 中最简洁的 Applet 之一。

## 选项

| 选项 | 描述 |
|------|------|
| `-n` | 不输出末尾的换行符 |

## 示例

```bash
# 基本用法
idlebox echo "Hello, World!"
# 输出: Hello, World!

# 多个参数（以空格连接）
idlebox echo Hello World
# 输出: Hello World

# 不输出末尾换行符
idlebox echo -n "no newline here"
# 输出: no newline here (光标停留在同一行)
```

## 实现说明

- 位于 `src/applets/echo.rs`
- 使用 Rust 标准库的 `println!` / `print!` 宏
- 参数之间以单个空格字符连接
- `-n` 标志必须作为第一个参数才能生效

## 参见

- [cat](cat.md) — 读取文件内容
- [架构概览](../architecture.md)
