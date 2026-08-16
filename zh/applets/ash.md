# ash — 指向 ish 的符号链接

> **其他语言：** [English](../../en/applets/ash.md)

`ash` 命令是指向 [ish](ish.md)（Idle Shell）的符号链接。

## 语法

```
ash [选项] [脚本]
ash -c 命令
```

## 描述

`ash` 命令提供与 `ish` 完全相同的功能。它为熟悉 Almquist Shell（`ash`）的用户提供便利。

完整文档请参见 [ish](ish.md)。

## 示例

```bash
# 执行命令
idlebox ash -c "echo hello"

# 执行脚本
idlebox ash script.sh

# 启动交互式 Shell
idlebox ash
```

## 参见

- [ish](ish.md) — 完整文档
- [sh](sh.md) — ish 的另一个别名
