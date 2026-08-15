# sleep — 暂停指定时长

> **其他语言：** [English](../../en/applets/sleep.md)

## 语法

```
sleep 数值[后缀]...
```

## 描述

`sleep` 按所有给定时间段之和暂停执行，数值可以是小数。

## 后缀

| 后缀 | 单位 |
|------|------|
| 无或 `s` | 秒 |
| `m` | 分钟 |
| `h` | 小时 |
| `d` | 天 |

## 示例

```bash
idlebox sleep 0.5
idlebox sleep 2m
idlebox sleep 1h 30m
```

## 实现说明

- 位于 `src/applets/sleep.rs`
- 使用 `std::thread::sleep` 与经过溢出检查的 `Duration` 加法
- 拒绝负数、非有限数、未知后缀和溢出的时间段

## 参见

- [relax](relax.md)
