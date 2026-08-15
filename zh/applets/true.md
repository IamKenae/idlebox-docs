# true — 返回成功

> **其他语言：** [English](../../en/applets/true.md)

## 语法

```
true
```

## 描述

`true` 不输出内容并返回退出状态 `0`。额外操作数会被忽略，适合 Shell 条件和占位命令。

## 示例

```bash
idlebox true
idlebox true && idlebox echo success
```

## 实现说明

- 位于 `src/applets/truth.rs`
- 正常执行时不分配内存，也不进行 I/O

## 参见

- [false](false.md)
- [test](test.md)
