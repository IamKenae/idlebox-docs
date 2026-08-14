# kill — 向进程发送信号

> **其他语言：** [English](../../en/applets/kill.md)

## 语法

```
kill [-SIGNAL] PID...
kill -s SIGNAL PID...
kill -l
```

## 描述

`kill` Applet 向指定进程发送 POSIX 信号。信号可以通过数字（如 `-9`）或名称（如 `-TERM`、`-KILL`、`-HUP`）指定。默认信号为 `SIGTERM`（15）。

## 选项

| 选项 | 描述 |
|------|------|
| `-SIGNAL` | 信号编号或名称（如 `-9`、`-TERM`、`-KILL`） |
| `-s SIGNAL` | 通过编号或名称指定信号 |
| `-l`, `--list` | 列出所有可用信号及其编号 |

## 支持的信号

| 编号 | 名称 | 描述 |
|------|------|------|
| 1 | HUP | 挂断 |
| 2 | INT | 中断（Ctrl+C） |
| 3 | QUIT | 退出 |
| 9 | KILL | 强制终止（不可捕获） |
| 15 | TERM | 终止（默认） |
| 17 | CHLD | 子进程状态变更 |
| 18 | CONT | 继续 |
| 19 | STOP | 停止（不可捕获） |
| 20 | TSTP | 终端停止 |

## 示例

```bash
# 向 PID 1234 发送 SIGTERM（默认）
idlebox kill 1234

# 向 PID 1234 发送 SIGKILL
idlebox kill -9 1234

# 通过名称发送 SIGKILL
idlebox kill -KILL 1234

# 使用 -s 选项发送信号
idlebox kill -s TERM 1234 5678

# 列出所有可用信号
idlebox kill -l
```

## 实现说明

- 位于 `src/applets/kill.rs`
- 通过 FFI 调用 POSIX `kill(pid, sig)` 系统调用
- 支持全部 31 个标准 POSIX 信号（1-31）
- 信号名称不区分大小写，可选包含 `SIG` 前缀

## 参见

- [ps](ps.md) — 报告进程状态
- [架构概览](../architecture.md)
