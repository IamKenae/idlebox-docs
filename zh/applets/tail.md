# tail — 输出文件的末尾部分

> **其他语言：** [English](../../en/applets/tail.md)

## 语法

```
tail [选项]... [文件]...
```

## 描述

`tail` Applet 输出文件的末尾部分。默认输出每个文件的最后 10 行。不指定文件或文件为 `-` 时，从标准输入读取。

## 选项

| 选项 | 描述 |
|------|------|
| `-n`, `--lines=N` | 输出最后 N 行（默认 10） |
| `-c`, `--bytes=N` | 输出最后 N 个字节 |

## 示例

```bash
# 显示最后 10 行（默认）
idlebox tail file.txt

# 显示最后 3 行
idlebox tail -n 3 file.txt

# 显示最后 50 字节
idlebox tail -c 50 file.txt

# 从 stdin 管道读取
echo -e "a\nb\nc\nd\ne" | idlebox tail -n 2
# 输出: d, e

# 处理多个文件时显示文件标头
idlebox tail -n 3 file1.txt file2.txt
# 输出:
# ==> file1.txt <==
# ...
# ==> file2.txt <==
# ...
```

## 实现说明

- 位于 `src/applets/tail.rs`
- 行模式使用环形缓冲区（Vec）实现内存高效的尾部读取
- 文件的字节模式使用 `seek` 从末尾定位，O(1) 复杂度
- stdin 的字节模式读取全部输入后提取尾部
- 处理多个文件时输出 `==> 文件名 <==` 标头
- 不指定文件或文件为 `-` 时，从 stdin 读取

## 参见

- [head](head.md) — 读取文件开头部分
- [cat](cat.md) — 读取整个文件
- [架构概览](../architecture.md)
