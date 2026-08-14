# relax — 休息一下

> **其他语言：** [English](../../en/applets/relax.md)

## 语法

```
relax [秒数]
```

## 描述

`relax` 是 IdleBox 的标志性 Applet —— 一个温柔的提醒，让你暂停片刻、放松身心。它会空闲指定的秒数，然后返回一条清新的消息。

这个 Applet 体现了 IdleBox 中 "Idle" 的真谛：有时候，最有效率的事情就是什么都不做。

## 参数

| 参数 | 描述 |
|------|------|
| `秒数` | 放松的持续时间，单位为秒（默认值：`5`） |

## 示例

```bash
# 默认：放松 5 秒
idlebox relax
# 输出:
# Relaxing for 5 seconds...
# (5 秒过去)
# Refreshed! Back to work.

# 放松 10 秒
idlebox relax 10
# 输出:
# Relaxing for 10 seconds...
# (10 秒过去)
# Refreshed! Back to work.
```

## 实现说明

- 位于 `src/applets/relax.rs`
- 使用 `std::thread::sleep` 实现等待
- 未提供参数时默认 5 秒
- 无效（非数字）参数会回退到默认的 5 秒
- 此 Applet 没有标志或选项 —— 纯粹的空闲体验

## 设计哲学

> **告别 Busy，拥抱 Idle。**

在一个痴迷于生产力的世界里，`relax` 是一次小小的反叛。它提醒我们：休息不是工作的对立面 —— 而是工作的基石。

## 参见

- [架构概览](../architecture.md)
