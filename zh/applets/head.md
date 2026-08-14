# head — 输出文件的开头部分

> **其他语言：** [English](../../en/applets/head.md)

## 语法

```
head [选项]... [文件]...
```

## 描述

`head` Applet 输出文件的开头部分。默认输出每个文件的前 10 行。不指定文件或文件为 `-` 时，从标准输入读取。

## 选项

| 选项 | 描述 |
|------|------|
| `-n`, `--lines=N` | 输出前 N 行（默认 10） |
| `-c`, `--bytes=N` | 输出前 N 个字节 |

## 示例

```bash
# 显示前 10 行（默认）
idlebox head file.txt

# 显示前 5 行
idlebox head -n 5 file.txt

# 显示前 100 字节
idlebox head -c 100 file.txt

# 从 stdin 管道读取
echo -e "a\nb\nc\nd\ne" | idlebox head -n 3
# 输出: a, b, c

# 处理多个文件时显示文件标头
idlebox head -n 3 file1.txt file2.txt
# 输出:
# ==> file1.txt <==
# ...
# ==> file2.txt <==
# ...
```

## 实现说明

- 位于 `src/applets/head.rs`
- 使用 `BufReader` 进行高效的逐行读取
- 字节模式使用 8KB 缓冲区的流式处理
- 处理多个文件时输出 `==> 文件名 <==` 标头
- 不指定文件或文件为 `-` 时，从 stdin 读取

## 参见

- [tail](tail.md) — 读取文件末尾部分
- [cat](cat.md) — 读取整个文件
- [架构概览](../architecture.md)
