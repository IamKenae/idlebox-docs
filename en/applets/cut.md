# cut — Remove Sections from Each Line of Files

> **Other languages:** [中文](../../zh/applets/cut.md)

## Synopsis

```
cut [OPTION]... [FILE]...
```

## Description

The `cut` applet prints selected parts of lines from each FILE to standard output. You can select fields (columns) delimited by a character, or select characters by position. With no FILE, or when FILE is `-`, it reads from standard input.

## Options

| Option | Description |
|--------|-------------|
| `-d`, `--delimiter=DELIM` | Use DELIM as the field delimiter (default: TAB) |
| `-f`, `--fields=LIST` | Select only these fields (e.g., `1`, `1,3`, `1-3`) |
| `-c`, `--characters=LIST` | Select only these characters (e.g., `1-5`) |

Field/character positions are 1-based. Ranges like `1-3` select positions 1 through 3. An open-ended range like `3-` selects from position 3 to end of line.

## Exit Status

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | Error occurred |

## Examples

```bash
# Extract first field from CSV
idlebox cut -d',' -f1 data.csv

# Extract fields 1 and 3
idlebox cut -d',' -f1,3 data.csv

# Extract a range of fields
idlebox cut -d',' -f1-3 data.csv

# Extract characters 1 through 5
idlebox cut -c1-5 file.txt

# Extract from colon-delimited /etc/passwd
idlebox cut -d: -f1 /etc/passwd

# From stdin pipe
echo "hello:world" | idlebox cut -d: -f2
# Output: world

# Multiple files
idlebox cut -d',' -f1 file1.csv file2.csv
```

## Implementation Notes

- Located in `src/applets/cut.rs`
- Default delimiter is TAB (matching POSIX behavior)
- Field/character positions are 1-based (matching POSIX convention)
- Overlapping ranges are deduplicated by position
- Open-ended ranges (e.g., `3-`) are supported

## See Also

- [sort](sort.md) — for sorting lines
- [grep](grep.md) — for pattern-based line selection
- [Architecture Overview](../architecture.md)
