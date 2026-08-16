# sh — Symbolic Link to ish

> **Other languages:** [中文](../../zh/applets/sh.md)

The `sh` command is a symbolic link to [ish](ish.md) (Idle Shell).

## Synopsis

```
sh [OPTIONS] [SCRIPT]
sh -c COMMAND
```

## Description

The `sh` command provides identical functionality to `ish`. It is provided as a convenience for users familiar with the traditional `sh` shell.

See [ish](ish.md) for complete documentation.

## Examples

```bash
# Execute a command
idlebox sh -c "echo hello"

# Execute a script
idlebox sh script.sh

# Start interactive shell
idlebox sh
```

## See Also

- [ish](ish.md) — Complete documentation
- [ash](ash.md) — Another alias to ish
