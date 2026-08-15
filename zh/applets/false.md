# false — 返回失败

> **其他语言：** [English](../../en/applets/false.md)

## 语法

```
false
```

## 描述

`false` 不输出内容并返回退出状态 `1`，额外操作数会被忽略。

## 示例

```bash
idlebox false
idlebox false || idlebox echo fallback
```

## 实现说明

- 位于 `src/applets/truth.rs`
- 正常执行时不分配内存，也不进行 I/O

## 参见

- [true](true.md)
- [test](test.md)
