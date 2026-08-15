# printf — 格式化并输出参数

> **其他语言：** [English](../../en/applets/printf.md)

## 语法

```
printf 格式 [参数]...
```

## 描述

`printf` 使用格式串处理参数；只要还有参数未消费，就会重复使用格式串，适配常见 Shell 与 BusyBox 工作流。

## 转换格式

| 转换 | 描述 |
|------|------|
| `%s`, `%c` | 字符串或首字符 |
| `%b` | 展开反斜杠转义的字符串；`\c` 停止输出 |
| `%d`, `%i`, `%u` | 有符号或无符号整数 |
| `%o`, `%x`, `%X` | 八进制或十六进制整数 |
| `%f`, `%e`, `%E`, `%g`, `%G` | 浮点格式 |
| `%%` | 百分号字面量 |

支持字段宽度、精度、`*` 动态宽度/精度，以及常用的 `#`、`-`、`+`、空格和 `0` 标志。

## 示例

```bash
idlebox printf '%s = %04d\n' answer 42
# answer = 0042

idlebox printf '[%s]' one two
# [one][two]

idlebox printf '%b' 'first\nsecond\n'
```

## 实现说明

- 位于 `src/applets/printf.rs`
- 通过小型解析器完成格式化，不引入 Applet 专用 crate
- 支持十进制、十六进制、八进制、引号字符数值参数和 C 风格转义

## 参见

- [echo](echo.md)
- [env](env.md)
