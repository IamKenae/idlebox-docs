# sh — 指向 ish 的符号链接

> **其他语言：** [English](../../en/applets/sh.md)

`sh` 命令是指向 [ish](ish.md)（Idle Shell）的符号链接。

## 语法

```
sh [选项] [脚本]
sh -c 命令
```

## 描述

`sh` 命令提供与 `ish` 完全相同的功能。它为熟悉传统 `sh` Shell 的用户提供便利。

完整文档请参见 [ish](ish.md)。

## 示例

```bash
# 执行命令
idlebox sh -c "echo hello"

# 执行脚本
idlebox sh script.sh

# 启动交互式 Shell
idlebox sh
```

## 参见

- [ish](ish.md) — 完整文档
- [ash](ash.md) — ish 的另一个别名
