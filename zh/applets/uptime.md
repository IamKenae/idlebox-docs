# uptime — 显示系统运行时间

> **其他语言：** [English](../../en/applets/uptime.md)

## 语法

```
uptime
```

## 描述

`uptime` Applet 显示当前时间、系统运行时长、用户数量以及过去 1、5、15 分钟的系统平均负载。数据从 `/proc/uptime` 和 `/proc/loadavg` 读取。

## 选项

此 Applet 无选项。

## 输出格式

```
2024-01-15 14:30:22  up 5 days, 03:42,  1 user,  load average: 0.15, 0.20, 0.18
```

## 示例

```bash
# 显示系统运行时间与平均负载
idlebox uptime
```

## 输出字段

| 字段 | 描述 |
|------|------|
| 当前时间 | 系统日期和时间（YYYY-MM-DD HH:MM:SS） |
| up X days, HH:MM | 自上次启动以来的运行时长 |
| 1 user | 已登录用户数（简化显示，默认为 1） |
| load average | 1、5、15 分钟系统平均负载 |

## 实现说明

- 位于 `src/applets/uptime.rs`
- 解析 `/proc/uptime` 获取系统运行秒数
- 解析 `/proc/loadavg` 获取 1/5/15 分钟平均负载及任务数
- 通过 FFI 调用 `gettimeofday` 系统调用获取当前时间
- 从 Unix 纪元天数计算日历日期，无需外部日期库

## 参见

- [ps](ps.md) — 报告进程状态
- [架构概览](../architecture.md)
