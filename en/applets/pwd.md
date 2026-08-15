# pwd — Print the Current Working Directory

> **Other languages:** [中文](../../zh/applets/pwd.md)

## Synopsis

```
pwd [-LP]
```

## Description

`pwd` prints the absolute current working directory. Logical mode preserves a valid `PWD` value; physical mode resolves symbolic links.

## Options

| Option | Description |
|--------|-------------|
| `-L`, `--logical` | Preserve a validated logical `PWD` path (default) |
| `-P`, `--physical` | Resolve symbolic links in the path |

When both forms are present, the last option takes effect.

## Examples

```bash
idlebox pwd
idlebox pwd -P
```

## Implementation Notes

- Located in `src/applets/pwd.rs`
- Validates that `PWD` is absolute, contains no `.` or `..` components, and resolves to the current directory

## See Also

- [realpath](realpath.md)
- [dirname](dirname.md)
