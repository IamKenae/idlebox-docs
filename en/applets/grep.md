# grep — Search for Patterns in Files or Standard Input

> **Other languages:** [中文](../../zh/applets/grep.md)

## Synopsis

```
grep [OPTION]... PATTERN [FILE]...
```

## Description

The `grep` applet searches for lines matching a pattern and outputs them. It supports case-insensitive matching, inverted matching, line numbering, count-only mode, and parallel multi-threaded search. With no file, or when the file is `-`, it reads from standard input.

## Options

| Option | Description |
|--------|-------------|
| `-i`, `--ignore-case` | Ignore case distinctions in pattern matching |
| `-v`, `--invert-match` | Select non-matching lines (invert the match) |
| `-n`, `--line-number` | Prefix each output line with its 1-based line number |
| `-c`, `--count` | Only print a count of matching lines per file |
| `-j`, `--threads N` | Use N threads for parallel search (default: auto-detect CPU cores) |

## Parallel Search Engine

The `-j` / `--threads` option enables parallel search across multiple files using Rust's standard library threading. When searching multiple files, the workload is distributed across worker threads for significantly improved performance on multi-core systems.

**Key features:**
- Automatic CPU core detection when `-j` is not specified
- Ordered result collection maintains POSIX-compatible output order
- Falls back to single-threaded mode for stdin or single file searches
- Thread count can be explicitly set with `-j N` (e.g., `-j 4` for 4 threads)

**Performance benefits:**
- Multi-file searches scale linearly with available CPU cores
- Large directory trees benefit from parallel I/O operations
- No external dependencies - pure Rust standard library implementation

## Exit Status

| Code | Meaning |
|------|---------|
| 0 | At least one match found |
| 1 | No matches found |
| 2 | Error occurred |

## Examples

```bash
# Basic pattern search
idlebox grep "error" log.txt

# Case-insensitive search
idlebox grep -i "error" log.txt

# Show line numbers
idlebox grep -n "TODO" source.rs

# Inverted match (show non-matching lines)
idlebox grep -v "debug" log.txt

# Count matching lines
idlebox grep -c "warning" log.txt

# Combined: case-insensitive with line numbers
idlebox grep -in "error" log.txt
# Output: 3:Error occurred
#         7:ERROR: fatal
#         12:error: minor

# Search from stdin pipe
cat log.txt | idlebox grep -i "error"

# Search multiple files
idlebox grep "pattern" file1.txt file2.txt
# Output: file1.txt:matching line
#         file2.txt:another match

# Parallel search with 4 threads
idlebox grep -j 4 "error" *.log

# Parallel search with automatic thread detection
idlebox grep -j 0 "pattern" /var/log/*.log
```

## Implementation Notes

- Located in `src/applets/grep.rs`
- Uses simple substring matching without a regex or applet-specific crate dependency
- Case-insensitive mode lowercases both pattern and line for comparison
- Returns exit code 0 on match, 1 on no match, 2 on error
- Multiple files prefix output with `filename:`
- Line numbers are 1-based (matching POSIX convention)
- When invoked without a pattern, prints usage information and exits with code 2
- Parallel engine uses `std::thread` and `std::sync` primitives (zero external dependencies)
- Work distribution uses atomic index tracking for optimal load balancing

## See Also

- [cat](cat.md) — for reading file contents
- [head](head.md) — for reading the beginning of files
- [tail](tail.md) — for reading the end of files
- [Architecture Overview](../architecture.md)
