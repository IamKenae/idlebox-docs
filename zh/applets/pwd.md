# pwd — 打印当前工作目录

> **其他语言：** [English](../../en/applets/pwd.md)

## 语法

```
pwd [-LP]
```

## 描述

`pwd` 打印当前工作目录的绝对路径。逻辑模式保留有效的 `PWD`，物理模式解析符号链接。

## 选项

| 选项 | 描述 |
|------|------|
| `-L`, `--logical` | 保留经过验证的逻辑 `PWD` 路径（默认） |
| `-P`, `--physical` | 解析路径中的符号链接 |

同时出现两种形式时，以最后一个选项为准。

## 示例

```bash
idlebox pwd
idlebox pwd -P
```

## 实现说明

- 位于 `src/applets/pwd.rs`
- 验证 `PWD` 必须为绝对路径、不含 `.` 或 `..`，且解析后确实指向当前目录

## 参见

- [realpath](realpath.md)
- [dirname](dirname.md)
