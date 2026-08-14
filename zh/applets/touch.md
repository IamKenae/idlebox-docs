# touch — 更新文件时间戳或创建空文件

> **其他语言：** [English](../../en/applets/touch.md)

## 语法

```
touch [选项]... 文件...
```

## 描述

`touch` Applet 在文件不存在时创建空文件，或在文件已存在时将其访问时间和修改时间更新为当前时间。

## 参数

| 参数 | 描述 |
|------|------|
| `文件...` | 一个或多个要创建或更新的文件路径 |

## 示例

```bash
# 创建单个空文件
idlebox touch newfile.txt

# 一次创建多个空文件
idlebox touch file1.txt file2.txt file3.txt

# 更新已有文件的时间戳
idlebox touch existing.txt

# 创建文件并立即使用
idlebox touch log.txt
idlebox echo "started" >> log.txt
```

## 实现说明

- 位于 `src/applets/touch.rs`
- 使用 `std::fs::File::create` 创建新文件
- 在 Unix 系统上使用 `utimes` 系统调用更新时间戳
- 多个文件按顺序处理，某个文件出错不影响其他文件
- 若任一操作失败，返回退出码 1

## 参见

- [cat](cat.md) — 读取文件内容
- [head](head.md) — 读取文件开头部分
- [tail](tail.md) — 读取文件末尾部分
- [架构概览](../architecture.md)
