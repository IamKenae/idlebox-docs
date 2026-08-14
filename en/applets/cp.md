# cp — Copy Files and Directories

> **Other languages:** [中文](../../zh/applets/cp.md)

## Synopsis

```
cp [OPTION]... SOURCE... DEST
```

## Description

The `cp` applet copies files and directories. Copying a single file to a destination creates or overwrites the destination file. When copying multiple sources or a directory, the destination must be a directory.

## Options

| Option | Description |
|--------|-------------|
| `-r`, `-R`, `--recursive` | Copy directories recursively |
| `-f`, `--force` | Force overwrite of existing destination files |

Options can be combined: `-rf`, `-fr`, etc.

## Examples

```bash
# Copy a single file
idlebox cp source.txt dest.txt

# Copy a file into a directory
idlebox cp file.txt target_dir/

# Copy multiple files into a directory
idlebox cp file1.txt file2.txt file3.txt target_dir/

# Recursively copy a directory
idlebox cp -r src_dir/ dst_dir/

# Force overwrite
idlebox cp -f source.txt dest.txt

# Recursive copy with force
idlebox cp -rf project/ backup/
```

## Implementation Notes

- Located in `src/applets/cp.rs`
- Uses `std::fs::copy` for files (preserves content, not metadata)
- Recursive directory copy walks the tree and recreates the full structure
- Without `-r`, attempting to copy a directory produces an error and skips it
- When multiple sources are given, the last argument is treated as the destination directory
- Returns exit code 1 if any copy operation fails

## See Also

- [mv](mv.md) — for moving files
- [rm](rm.md) — for removing files
- [Architecture Overview](../architecture.md)
