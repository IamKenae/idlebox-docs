# dirname — 去除文件名的最后一部分

> **其他语言：** [English](../../en/applets/dirname.md)

## 语法

```
dirname [选项] 名称...
```

## 描述

`dirname` 去除每个名称最后的路径组成部分。名称中没有目录时输出 `.`。

## 选项

| 选项 | 描述 |
|------|------|
| `-z`, `--zero` | 使用 NUL 而不是换行符结束记录 |

## 示例

```bash
idlebox dirname /usr/local/bin/tool
# /usr/local/bin

idlebox dirname file.txt
# .
```

## 实现说明

- 位于 `src/applets/dirname.rs`
- 以词法方式处理路径，不要求路径实际存在
- 一次调用可处理多个名称

## 参见

- [basename](basename.md)
- [pwd](pwd.md)
