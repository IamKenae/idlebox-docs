# find — Search for Files

> **Other languages:** [中文](../../zh/applets/find.md)

## Synopsis

```
find [PATH...] [OPTIONS]
```

## Description

The `find` applet recursively searches directory hierarchies for files matching specified criteria. If no path is given, it defaults to the current directory (`.`).

## Options

| Option | Description |
|--------|-------------|
| `-name PATTERN` | Match file name with glob pattern (e.g., `*.rs`, `test_??.txt`) |
| `-type TYPE` | Filter by type: `f` (regular file), `d` (directory), `l` (symbolic link) |
| `-maxdepth N` | Limit recursion depth (0 = only the starting path) |
| `-empty` | Match only empty files or empty directories |

## Glob Pattern Syntax

The `-name` option supports simple glob patterns:
- `*` matches any sequence of characters
- `?` matches any single character
- All other characters match literally

## Examples

```bash
# Find all Rust source files
idlebox find . -name "*.rs"

# Find all directories
idlebox find /tmp -type d

# Find files with max depth
idlebox find . -name "*.txt" -maxdepth 2

# Find empty files and directories
idlebox find . -empty

# Combine options
idlebox find . -type f -name "*.log" -empty

# Find symbolic links
idlebox find /usr -type l
```

## Implementation Notes

- Located in `src/applets/find.rs`
- Uses `std::fs::read_dir` for directory traversal
- Glob matching implemented with a simple state machine (no external regex library)
- Results are sorted alphabetically within each directory level
- Uses `symlink_metadata` to correctly identify symbolic links without following them
- Uses only Rust standard library

## See Also

- [ls](ls.md) — list directory contents
- [test](test.md) — file test operators
- [Architecture Overview](../architecture.md)
