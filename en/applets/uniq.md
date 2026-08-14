# uniq — Report or Omit Repeated Lines

> **Other languages:** [中文](../../zh/applets/uniq.md)

## Synopsis

```
uniq [OPTION]... [INPUT [OUTPUT]]
```

## Description

The `uniq` applet filters adjacent matching lines from INPUT (or standard input), writing to stdout. By default, it collapses runs of identical lines into a single output line. Note that `uniq` only detects lines that are adjacent — consider using `sort` first if your input is not already grouped.

## Options

| Option | Description |
|--------|-------------|
| `-c`, `--count` | Prefix each line with the number of occurrences |
| `-d`, `--repeated` | Only print lines that are repeated (appear more than once) |
| `-u`, `--unique` | Only print lines that appear exactly once |
| `-i`, `--ignore-case` | Ignore case when comparing lines |

## Exit Status

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | Error occurred |

## Examples

```bash
# Remove adjacent duplicates
idlebox uniq file.txt

# Count occurrences
idlebox uniq -c file.txt
# Output:
#       2 apple
#       3 banana
#       1 cherry

# Only show repeated lines
idlebox uniq -d file.txt

# Only show unique (non-repeated) lines
idlebox uniq -u file.txt

# Case-insensitive comparison
idlebox uniq -i file.txt

# Combine count with repeated filter
idlebox uniq -c -d file.txt
# Output:
#       2 apple
#       3 banana

# From stdin pipe
cat file.txt | idlebox uniq -c
```

## Implementation Notes

- Located in `src/applets/uniq.rs`
- Only detects adjacent duplicate lines (POSIX behavior)
- Count output is right-aligned with 7-character-wide column
- Case-insensitive mode lowercases both lines for comparison
- Reads all lines into memory before processing

## See Also

- [sort](sort.md) — sort lines before uniq to remove all duplicates
- [wc](wc.md) — for counting lines
- [Architecture Overview](../architecture.md)
