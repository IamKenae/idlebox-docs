# chgrp — Change Group Ownership

> **Other languages:** [中文](../../zh/applets/chgrp.md)

## Synopsis

```
chgrp [-R] GROUP FILE...
```

## Description

The `chgrp` applet changes the group ownership of each given file. The group may be specified by name or numeric GID.

## Options

| Option | Description |
|--------|-------------|
| `-R`, `--recursive` | Change files and directories recursively |

## Examples

```bash
# Change group to "users"
idlebox chgrp users file.txt

# Change group using numeric GID
idlebox chgrp 1000 file.txt

# Recursively change group of a directory
idlebox chgrp -R users mydir/

# Change group of multiple files
idlebox chgrp users file1.txt file2.txt
```

## Implementation Notes

- Located in `src/applets/chgrp.rs`
- Uses POSIX `chown()` and `lchown()` FFI calls (with UID unchanged)
- Symlinks are handled via `lchown()` (does not follow symlinks)
- No applet-specific crate dependency — Rust standard library + POSIX libc FFI

## See Also

- [chown](chown.md) — change file owner and group
- [chmod](chmod.md) — change file mode bits
- [ls](ls.md) — view file ownership
- [Architecture Overview](../architecture.md)
