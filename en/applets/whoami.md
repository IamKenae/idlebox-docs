# whoami — Print Effective User Name

> **Other languages:** [中文](../../zh/applets/whoami.md)

## Synopsis

```
whoami
```

## Description

The `whoami` applet prints the effective user name of the current user. It is equivalent to `id -un`.

## Options

None.

## Examples

```bash
# Print the current effective user name
idlebox whoami
```

## Implementation Notes

- Located in `src/applets/whoami.rs`
- Uses POSIX `geteuid()` and `getpwuid()` FFI calls
- No applet-specific crate dependency — Rust standard library + POSIX libc FFI

## See Also

- [id](id.md) — print real and effective user and group IDs
- [Architecture Overview](../architecture.md)
