# printenv — 打印环境变量

> **其他语言：** [English](../../en/applets/printenv.md)

## 语法

```
printenv [选项]... [变量]...
```

## 描述

不带操作数时，`printenv` 以 `名称=值` 的形式打印全部环境；给出变量名时，按照请求顺序只打印对应的值。

## 选项

| 选项 | 描述 |
|------|------|
| `-0`, `--null` | 使用 NUL 结束每条输出记录 |

## 示例

```bash
idlebox printenv PATH
idlebox printenv HOME USER
idlebox printenv -0
```

## 退出状态

任一请求的变量不存在时返回 `1`，同时仍会输出其他存在的变量。

## 实现说明

- 位于 `src/applets/printenv.rs`
- 将变量值直接流式写入标准输出

## 参见

- [env](env.md)
