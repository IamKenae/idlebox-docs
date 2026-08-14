# mv — Move (Rename) Files and Directories

> **Other languages:** [中文](../../zh/applets/mv.md)

## Synopsis

```
mv [OPTION]... SOURCE... DEST
```

## Description

The `mv` applet moves or renames files and directories. When the destination is an existing directory, sources are moved into it. When there is a single source and the destination is not a directory, the source is renamed.

## Behavior

- Renames files and directories: `mv old.txt new.txt`
- Moves multiple items into a directory: `mv f1 f2 target_dir/`
- Overwrites existing files by default (no prompt)
- **Cross-device support**: if `rename()` fails with `EXDEV` (cross-device link), automatically falls back to copy + delete

## Examples

```bash
# Rename a file
idlebox mv old_name.txt new_name.txt

# Move a file into a directory
idlebox mv file.txt target_dir/

# Move multiple files into a directory
idlebox mv file1.txt file2.txt file3.txt target_dir/

# Rename a directory
idlebox mv old_dir/ new_dir/

# Move a directory into another directory
idlebox mv mydir/ target_parent/
```

## Implementation Notes

- Located in `src/applets/mv.rs`
- Uses `std::fs::rename` as the primary mechanism (atomic on same filesystem)
- On `EXDEV` error (cross-device), falls back to recursive copy + delete
- Cross-device fallback handles both files and directories
- When multiple sources are given, the last argument is treated as the destination directory
- Returns exit code 1 if any move operation fails

## See Also

- [cp](cp.md) — for copying files
- [rm](rm.md) — for removing files
- [Architecture Overview](../architecture.md)
