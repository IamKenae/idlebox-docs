# sort — Sort Lines of Text Files

> **Other languages:** [中文](../../zh/applets/sort.md)

## Synopsis

```
sort [OPTION]... [FILE]...
```

## Description

The `sort` applet writes sorted concatenation of all FILEs to standard output. With no FILE, or when FILE is `-`, it reads from standard input. Multiple files are merged and sorted together.

## Options

| Option | Description |
|--------|-------------|
| `-r`, `--reverse` | Reverse the result of comparisons (descending order) |
| `-n`, `--numeric-sort` | Compare according to string numerical value |
| `-u`, `--unique` | Output only unique lines (remove duplicates) |

## Exit Status

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | Error occurred |

## Examples

```bash
# Basic alphabetical sort
idlebox sort file.txt

# Numeric sort
idlebox sort -n numbers.txt

# Reverse (descending) sort
idlebox sort -r file.txt

# Numeric descending sort
idlebox sort -n -r numbers.txt

# Sort and remove duplicates
idlebox sort -u file.txt

# Sort from stdin pipe
cat file.txt | idlebox sort

# Merge and sort multiple files
idlebox sort file1.txt file2.txt
```

## Implementation Notes

- Located in `src/applets/sort.rs`
- Numeric sort parses each line as f64; non-numeric lines sort as 0
- Unique mode uses `dedup()` after sorting (removes adjacent duplicates)
- Multiple files are read into a single buffer and sorted together
- Default sort is lexicographic (byte-wise comparison)

## See Also

- [uniq](uniq.md) — for filtering duplicate lines
- [wc](wc.md) — for counting lines
- [Architecture Overview](../architecture.md)
