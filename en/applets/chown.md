# chown — Change File Owner and Group

> **Other languages:** [中文](../../zh/applets/chown.md)

## Synopsis

```
chown [-R] [OWNER][:[GROUP]] FILE...
```

## Description

The `chown` applet changes the user and/or group ownership of each given file. The owner and group may be specified by name or numeric ID.

## Options

| Option | Description |
|--------|-------------|
| `-R`, `--recursive` | Change files and directories recursively |

## Owner/Group Specification

| Syntax | Description |
|--------|-------------|
| `user` | Change owner to `user`, keep current group |
| `user:group` | Change owner to `user` and group to `group` |
| `:group` | Keep current owner, change group to `group` |
| `user:` | Change owner to `user`, set group to user's login group |
| `1000:1000` | Use numeric UID and GID |

## Examples

```bash
# Change file owner to root
idlebox chown root file.txt

# Change owner and group
idlebox chown user:group file.txt

# Change only the group
idlebox chown :group file.txt

# Recursively change ownership of a directory
idlebox chown -R user:group mydir/

# Use numeric IDs
idlebox chown 1000:1000 file.txt
```

## Implementation Notes

- Located in `src/applets/chown.rs`
- Uses POSIX `chown()` and `lchown()` FFI calls
- Symlinks are handled via `lchown()` (does not follow symlinks)
- No applet-specific crate dependency — Rust standard library + POSIX libc FFI

## See Also

- [chgrp](chgrp.md) — change group ownership
- [chmod](chmod.md) — change file mode bits
- [ls](ls.md) — view file ownership
- [Architecture Overview](../architecture.md)
