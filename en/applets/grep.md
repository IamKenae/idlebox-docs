# grep — Search for Patterns in Files or Standard Input

> **Other languages:** [中文](../../zh/applets/grep.md)

## Synopsis

```
grep [OPTION]... PATTERN [FILE]...
```

## Description

The `grep` applet searches for lines matching a pattern and outputs them. It supports case-insensitive matching, inverted matching, line numbering, and count-only mode. With no file, or when the file is `-`, it reads from standard input.

## Options

| Option | Description |
|--------|-------------|
| `-i`, `--ignore-case` | Ignore case distinctions in pattern matching |
| `-v`, `--invert-match` | Select non-matching lines (invert the match) |
| `-n`, `--line-number` | Prefix each output line with its 1-based line number |
| `-c`, `--count` | Only print a count of matching lines per file |

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
```

## Implementation Notes

- Located in `src/applets/grep.rs`
- Uses simple substring matching without a regex or applet-specific crate dependency
- Case-insensitive mode lowercases both pattern and line for comparison
- Returns exit code 0 on match, 1 on no match, 2 on error
- Multiple files prefix output with `filename:`
- Line numbers are 1-based (matching POSIX convention)

## See Also

- [cat](cat.md) — for reading file contents
- [head](head.md) — for reading the beginning of files
- [tail](tail.md) — for reading the end of files
- [Architecture Overview](../architecture.md)
