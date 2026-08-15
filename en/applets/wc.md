# wc — Print Newline, Word, and Byte Counts for Each File

> **Other languages:** [中文](../../zh/applets/wc.md)

## Synopsis

```
wc [OPTION]... [FILE]...
```

## Description

The `wc` applet prints newline, word, and byte counts for each file. With no FILE, or when FILE is `-`, it reads from standard input. When multiple files are given, a `total` summary line is printed at the end. Supports parallel multi-threaded counting for improved performance with multiple files.

## Options

| Option | Description |
|--------|-------------|
| `-l`, `--lines` | Print the newline count |
| `-w`, `--words` | Print the word count |
| `-c`, `--bytes` | Print the byte count |
| `-m`, `--chars` | Print the character count |
| `-j`, `--threads N` | Use N threads for parallel counting (default: auto-detect CPU cores) |

When no options are specified, `wc` defaults to printing lines, words, and bytes.

## Parallel Counting Engine

The `-j` / `--threads` option enables parallel file counting using Rust's standard library threading. When processing multiple files, the workload is distributed across worker threads for significantly improved throughput.

**Key features:**
- Automatic CPU core detection when `-j` is not specified
- Ordered result collection maintains correct per-file output order
- Accurate total calculation across all threads
- Falls back to single-threaded mode for stdin or single file
- Thread count can be explicitly set with `-j N` (e.g., `-j 4` for 4 threads)

**Performance benefits:**
- Multi-file counting scales linearly with available CPU cores
- Large files benefit from parallel I/O operations
- No external dependencies - pure Rust standard library implementation

## Exit Status

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | Error occurred |

## Examples

```bash
# Count lines in a file
idlebox wc -l file.txt

# Count words in a file
idlebox wc -w file.txt

# Count bytes in a file
idlebox wc -c file.txt

# Default: lines, words, bytes
idlebox wc file.txt

# Count from stdin pipe
cat file.txt | idlebox wc -l

# Multiple files (shows total)
idlebox wc -l file1.txt file2.txt
# Output:
#       3 file1.txt
#       5 file2.txt
#       8 total

# Parallel counting with 4 threads
idlebox wc -l -j 4 *.txt

# Parallel counting with automatic thread detection
idlebox wc -j 8 file1.txt file2.txt file3.txt
```

## Implementation Notes

- Located in `src/applets/wc.rs`
- Reads in fixed 8 KiB chunks instead of buffering the entire file
- Skips Unicode decoding when only byte and/or newline counts are requested
- Preserves character and Unicode-whitespace word counting across UTF-8 chunk boundaries; invalid sequences follow lossy replacement semantics
- Multiple files produce a `total` summary line
- Output is right-aligned with 7-character-wide columns
- Parallel engine uses `std::thread` and `std::sync` primitives (zero external dependencies)
- Work distribution uses atomic index tracking for optimal load balancing

## See Also

- [cat](cat.md) — for reading file contents
- [sort](sort.md) — for sorting lines
- [Architecture Overview](../architecture.md)
