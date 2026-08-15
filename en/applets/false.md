# false — Return Failure

> **Other languages:** [中文](../../zh/applets/false.md)

## Synopsis

```
false
```

## Description

`false` produces no output and returns exit status `1`. Extra operands are ignored.

## Examples

```bash
idlebox false
idlebox false || idlebox echo fallback
```

## Implementation Notes

- Located in `src/applets/truth.rs`
- Performs no allocation or I/O during normal execution

## See Also

- [true](true.md)
- [test](test.md)
