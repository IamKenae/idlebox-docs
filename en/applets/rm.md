# rm — Remove Files or Directories

> **Other languages:** [中文](../../zh/applets/rm.md)

## Synopsis

```
rm [OPTION]... FILE...
```

## Description

The `rm` applet removes files and, with `-r`, directories and their contents recursively. Without `-r`, directories are not removed.

## Options

| Option | Description |
|--------|-------------|
| `-r`, `-R`, `--recursive` | Remove directories and their contents recursively |
| `-f`, `--force` | Ignore nonexistent files and arguments; never prompt |

Options can be combined: `-rf`, `-fr`, `-Rf`, or individual flags like `-r -f`.

## Examples

```bash
# Remove a single file
idlebox rm file.txt

# Remove multiple files
idlebox rm file1.txt file2.txt file3.txt

# Remove a directory and all its contents
idlebox rm -r mydir

# Force-remove without errors on missing files
idlebox rm -f nonexistent.txt

# Recursively force-remove (common cleanup pattern)
idlebox rm -rf build/ dist/

# Remove without -r fails on directories
idlebox rm mydir
# Error: Is a directory
```

## Implementation Notes

- Located in `src/applets/rm.rs`
- Uses `std::fs::remove_file` for files and `std::fs::remove_dir_all` for directories
- Without `-r`, attempting to remove a directory produces an error and returns exit code 1
- With `-f`, nonexistent paths are silently skipped
- Supports combined short flags (e.g., `-rf`)

## See Also

- [mkdir](mkdir.md) — for creating directories
- [cp](cp.md) — for copying files
- [Architecture Overview](../architecture.md)
