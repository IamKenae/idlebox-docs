# basename — 去除文件名中的目录与后缀

> **其他语言：** [English](../../en/applets/basename.md)

## 语法

```
basename 名称 [后缀]
basename 选项... 名称...
```

## 描述

`basename` 去除每个名称开头的目录部分，也可以删除匹配的末尾后缀，但不会把整个结果删空。

## 选项

| 选项 | 描述 |
|------|------|
| `-a`, `--multiple` | 处理全部“名称”操作数 |
| `-s`, `--suffix=后缀` | 删除后缀，同时隐含 `-a` |
| `-z`, `--zero` | 使用 NUL 而不是换行符结束记录 |

## 示例

```bash
idlebox basename /usr/local/bin/tool
# tool

idlebox basename report.txt .txt
# report

idlebox basename -s .log one.log /tmp/two.log
# one
# two
```

## 实现说明

- 位于 `src/applets/basename.rs`
- 只做词法路径处理，不访问文件系统
- 同时支持传统的“名称 [后缀]”形式和 GNU 风格多操作数

## 参见

- [dirname](dirname.md)
- [realpath](realpath.md)
