# find — Search for Files

> **Other languages:** [中文](../../zh/applets/find.md)

## Synopsis

```
find [PATH...] [OPTIONS]
```

## Description

The `find` applet recursively searches directory hierarchies for files matching specified criteria. If no path is given, it defaults to the current directory (`.`). Supports parallel multi-threaded traversal for improved performance on large directory trees.

## Options

| Option | Description |
|--------|-------------|
| `-name PATTERN` | Match file name with glob pattern (e.g., `*.rs`, `test_??.txt`) |
| `-type TYPE` | Filter by type: `f` (regular file), `d` (directory), `l` (symbolic link) |
| `-maxdepth N` | Limit recursion depth (0 = only the starting path) |
| `-empty` | Match only empty files or empty directories |
| `-j`, `--threads N` | Use N threads for parallel directory traversal (default: auto-detect CPU cores) |

## Parallel Directory Walker

The `-j` / `--threads` option enables parallel directory traversal using Rust's standard library threading. When searching deep or large directory trees, the workload is distributed across worker threads for significantly reduced I/O wait times.

**Key features:**
- Automatic CPU core detection when `-j` is not specified
- Dynamic work stealing from shared queue for optimal load balancing
- Sorted output maintains deterministic results across runs
- Falls back to single-threaded mode when `-j 1` is specified
- Thread count can be explicitly set with `-j N` (e.g., `-j 8` for 8 threads)

**Performance benefits:**
- Deep directory trees benefit from parallel I/O operations
- Multi-level hierarchies scale linearly with available CPU cores
- No external dependencies - pure Rust standard library implementation

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

# Parallel search with 4 threads
idlebox find . -name "*.rs" -j 4

# Parallel search with automatic thread detection
idlebox find /var -type f -j 8
```

## Implementation Notes

- Located in `src/applets/find.rs`
- Uses `std::fs::read_dir` for directory traversal
- Glob matching implemented with a simple state machine (no external regex library)
- Results are sorted alphabetically within each directory level
- Uses `symlink_metadata` to correctly identify symbolic links without following them
- Uses only Rust standard library
- Parallel engine uses work-stealing queue with atomic active thread tracking
- Thread synchronization via `std::sync::Mutex` and `std::sync::Arc`

## See Also

- [ls](ls.md) — list directory contents
- [test](test.md) — file test operators
- [Architecture Overview](../architecture.md)
