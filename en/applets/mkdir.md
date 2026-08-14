# mkdir — Create Directories

> **Other languages:** [中文](../../zh/applets/mkdir.md)

## Synopsis

```
mkdir [OPTION]... DIRECTORY...
```

## Description

The `mkdir` applet creates one or more directories. By default, parent directories must already exist. Use `-p` to create intermediate directories as needed.

## Options

| Option | Description |
|--------|-------------|
| `-p`, `--parents` | Create parent directories as needed; no error if the directory already exists |

## Examples

```bash
# Create a single directory
idlebox mkdir mydir

# Create nested directories (fails if parents don't exist)
idlebox mkdir a/b/c
# Error: No such file or directory

# Create nested directories with -p
idlebox mkdir -p a/b/c

# Create multiple directories at once
idlebox mkdir dir1 dir2 dir3

# Combined: create multiple nested paths
idlebox mkdir -p project/src project/tests project/docs/api
```

## Implementation Notes

- Located in `src/applets/mkdir.rs`
- Uses `std::fs::create_dir` (default) and `std::fs::create_dir_all` (with `-p`)
- Multiple directories are processed sequentially; errors in one do not prevent others from being created
- Returns exit code 1 if any directory creation fails

## See Also

- [rm](rm.md) — for removing directories
- [Architecture Overview](../architecture.md)
