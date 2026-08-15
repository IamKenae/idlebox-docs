# realpath — Print Canonical Absolute Paths

> **Other languages:** [中文](../../zh/applets/realpath.md)

## Synopsis

```
realpath [OPTION]... FILE...
```

## Description

`realpath` resolves every symbolic link and relative component, then prints a canonical absolute path. Every path component must exist.

## Options

| Option | Description |
|--------|-------------|
| `-e`, `--canonicalize-existing` | Require every component to exist (the default behavior) |
| `-q`, `--quiet` | Suppress diagnostics for paths that cannot be resolved |
| `-z`, `--zero` | End each output record with NUL |

## Examples

```bash
idlebox realpath ./src/../README.md
idlebox realpath -q missing-file
idlebox realpath -z path-one path-two
```

## Implementation Notes

- Located in `src/applets/realpath.rs`
- Uses `std::fs::canonicalize`, matching `readlink -f` for existing paths
- Continues processing remaining operands after an error

## See Also

- [readlink](readlink.md)
- [pwd](pwd.md)
