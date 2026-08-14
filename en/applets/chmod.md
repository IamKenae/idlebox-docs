# chmod — Change File Mode Bits

> **Other languages:** [中文](../../zh/applets/chmod.md)

## Synopsis

```
chmod [-R] MODE FILE...
```

## Description

The `chmod` applet changes the file permission bits of specified files or directories. It supports octal numeric mode (e.g. `755`, `0644`).

## Options

| Option | Description |
|--------|-------------|
| `-R`, `--recursive` | Change files and directories recursively |

## Examples

```bash
# Set file to 755 (rwxr-xr-x)
idlebox chmod 755 script.sh

# Set multiple files to 0644 (rw-r--r--)
idlebox chmod 0644 file1.txt file2.txt

# Recursively set directory permissions
idlebox chmod -R 755 mydir/
```

## Implementation Notes

- Located in `src/applets/chmod.rs`
- Uses `std::os::unix::fs::PermissionsExt` from the Rust standard library
- Mode is parsed as an octal number (base 8)
- Recursive mode traverses all entries within a directory

## See Also

- [ls](ls.md) — view file permissions
- [Architecture Overview](../architecture.md)
