# ash — Symbolic Link to ish

> **Other languages:** [中文](../../zh/applets/ash.md)

The `ash` command is a symbolic link to [ish](ish.md) (Idle Shell).

## Synopsis

```
ash [OPTIONS] [SCRIPT]
ash -c COMMAND
```

## Description

The `ash` command provides identical functionality to `ish`. It is provided as a convenience for users familiar with the Almquist shell (`ash`).

See [ish](ish.md) for complete documentation.

## Examples

```bash
# Execute a command
idlebox ash -c "echo hello"

# Execute a script
idlebox ash script.sh

# Start interactive shell
idlebox ash
```

## See Also

- [ish](ish.md) — Complete documentation
- [sh](sh.md) — Another alias to ish
