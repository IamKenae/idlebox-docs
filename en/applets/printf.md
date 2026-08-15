# printf — Format and Print Arguments

> **Other languages:** [中文](../../zh/applets/printf.md)

## Synopsis

```
printf FORMAT [ARGUMENT]...
```

## Description

`printf` applies a format string to its arguments. The format is reused until all arguments are consumed, matching common shell and BusyBox workflows.

## Conversions

| Conversion | Description |
|------------|-------------|
| `%s`, `%c` | String or first character |
| `%b` | String with backslash escapes expanded; `\c` stops output |
| `%d`, `%i`, `%u` | Signed or unsigned integer |
| `%o`, `%x`, `%X` | Octal or hexadecimal integer |
| `%f`, `%e`, `%E`, `%g`, `%G` | Floating-point formats |
| `%%` | Literal percent sign |

Field width, precision, `*` width/precision, and the common `#`, `-`, `+`, space, and `0` flags are supported.

## Examples

```bash
idlebox printf '%s = %04d\n' answer 42
# answer = 0042

idlebox printf '[%s]' one two
# [one][two]

idlebox printf '%b' 'first\nsecond\n'
```

## Implementation Notes

- Located in `src/applets/printf.rs`
- Formats directly from a small parser without external dependencies
- Supports decimal, hexadecimal, octal, quoted-character numeric operands, and C-style escapes

## See Also

- [echo](echo.md)
- [env](env.md)
