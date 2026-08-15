# tee — 将标准输入复制到文件和标准输出

> **其他语言：** [English](../../en/applets/tee.md)

## 语法

```
tee [选项]... [文件]...
```

## 描述

`tee` 只读取一次标准输入，并将每个数据块同时复制到标准输出和全部指定文件。

## 选项

| 选项 | 描述 |
|------|------|
| `-a`, `--append` | 追加内容而不是覆盖文件 |
| `-i`, `--ignore-interrupts` | 在 Unix-like 系统忽略中断信号 |

## 示例

```bash
idlebox printf 'hello\n' | idlebox tee output.txt
idlebox printf 'again\n' | idlebox tee -a output.txt
idlebox cat input.bin | idlebox tee copy-one.bin copy-two.bin >/dev/null
```

## 实现说明

- 位于 `src/applets/tee.rs`
- 使用固定的 16 KiB 流式缓冲区
- 标准输出管道提前关闭后仍继续写入文件
- 单个文件打开或写入失败时报告错误，并继续处理其他目标

## 参见

- [cat](cat.md)
- [printf](printf.md)
