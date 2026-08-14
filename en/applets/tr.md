# tr — Translate or Delete Characters

> **Other languages:** [中文](../../zh/applets/tr.md)

## Synopsis

```
tr [OPTION]... SET1 [SET2]
```

## Description

The `tr` applet reads from standard input and writes to standard output. It can translate characters from SET1 to SET2, delete characters matching SET1, or squeeze repeated characters.

Character sets support range expansion: `a-z` expands to all lowercase letters, `0-9` to all digits, etc.

## Options

| Option | Description |
|--------|-------------|
| `-d`, `--delete` | Delete characters in SET1 |
| `-s`, `--squeeze-repeats` | Replace each sequence of a repeated character with a single occurrence |

## Exit Status

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | Error occurred |

## Examples

```bash
# Convert lowercase to uppercase
echo "hello" | idlebox tr a-z A-Z
# Output: HELLO

# Delete digits
echo "abc123def" | idlebox tr -d 0-9
# Output: abcdef

# Delete carriage returns
echo -e "hello\r\nworld" | idlebox tr -d '\r'

# Squeeze repeated spaces
echo "hello    world" | idlebox tr -s ' '
# Output: hello world

# Translate and squeeze
echo "aabbcc" | idlebox tr -s a-c x
# Output: xxx

# ROT13-like transformation
echo "hello" | idlebox tr a-z n-za-m
# Output: uryyb
```

## Implementation Notes

- Located in `src/applets/tr.rs`
- Always reads from stdin (no file arguments)
- Character ranges like `a-z` are expanded to individual characters
- When SET2 is shorter than SET1, the last character of SET2 is repeated
- Squeeze mode compresses consecutive matching characters into one
- Delete mode removes all characters in SET1

## See Also

- [sed](cat.md) — for more complex text transformations
- [cat](cat.md) — for reading file contents
- [Architecture Overview](../architecture.md)
