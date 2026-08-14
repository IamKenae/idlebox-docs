# wc — Print Newline, Word, and Byte Counts for Each File

> **Other languages:** [中文](../../zh/applets/wc.md)

## Synopsis

```
wc [OPTION]... [FILE]...
```

## Description

The `wc` applet prints newline, word, and byte counts for each file. With no FILE, or when FILE is `-`, it reads from standard input. When multiple files are given, a `total` summary line is printed at the end.

## Options

| Option | Description |
|--------|-------------|
| `-l`, `--lines` | Print the newline count |
| `-w`, `--words` | Print the word count |
| `-c`, `--bytes` | Print the byte count |
| `-m`, `--chars` | Print the character count |

When no options are specified, `wc` defaults to printing lines, words, and bytes.

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
```

## Implementation Notes

- Located in `src/applets/wc.rs`
- Reads entire file into memory for accurate byte/char counting
- Words are counted using whitespace splitting (matching POSIX behavior)
- Multiple files produce a `total` summary line
- Output is right-aligned with 7-character-wide columns

## See Also

- [cat](cat.md) — for reading file contents
- [sort](sort.md) — for sorting lines
- [Architecture Overview](../architecture.md)
