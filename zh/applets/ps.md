# ps — 报告当前进程快照

> **其他语言：** [English](../../en/applets/ps.md)

## 语法

```
ps [-e] [-A] [-o COL1,COL2,...]
```

## 描述

`ps` Applet 显示当前运行进程的快照。它从 `/proc` 文件系统读取进程信息，解析每个进程的 `/proc/[pid]/stat` 和 `/proc/[pid]/cmdline`。

## 选项

| 选项 | 描述 |
|------|------|
| `-e`, `-A` | 显示所有进程（默认仅显示当前会话） |
| `-o COL1,COL2,...` | 自定义输出列 |

### 可用列

| 列名 | 描述 |
|------|------|
| `pid` | 进程 ID |
| `tty` | 控制终端 |
| `stat` | 进程状态（R=运行中，S=睡眠，Z=僵尸等） |
| `time` | 累计 CPU 时间 |
| `cmd` | 完整命令行及参数 |

## 输出格式

```
     PID TTY      STAT       TIME COMMAND
       1 ?        S        00:03 /sbin/init
     123 pts/0    S        00:00 bash
```

## 示例

```bash
# 显示所有进程
idlebox ps -e

# 仅显示当前会话进程
idlebox ps

# 自定义列：仅显示 PID 和命令
idlebox ps -e -o pid,cmd
```

## 实现说明

- 位于 `src/applets/ps.rs`
- 解析 `/proc/[pid]/stat` 获取进程状态、终端和 CPU 时间
- 解析 `/proc/[pid]/cmdline` 获取完整命令行
- 优雅处理枚举过程中消失的进程（ENOENT）
- 优雅处理受限 `/proc` 条目的权限不足错误

## 参见

- [kill](kill.md) — 向进程发送信号
- [架构概览](../architecture.md)
