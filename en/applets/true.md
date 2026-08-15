# true — Return Success

> **Other languages:** [中文](../../zh/applets/true.md)

## Synopsis

```
true
```

## Description

`true` produces no output and returns exit status `0`. Extra operands are ignored, making it suitable for shell conditions and placeholders.

## Examples

```bash
idlebox true
idlebox true && idlebox echo success
```

## Implementation Notes

- Located in `src/applets/truth.rs`
- Performs no allocation or I/O during normal execution

## See Also

- [false](false.md)
- [test](test.md)
