# tail — Output the Last Part of Files

> **Other languages:** [中文](../../zh/applets/tail.md)

## Synopsis

```
tail [OPTION]... [FILE]...
```

## Description

The `tail` applet outputs the last part of files. By default, it prints the last 10 lines of each file. With no file, or when the file is `-`, it reads from standard input.

## Options

| Option | Description |
|--------|-------------|
| `-n`, `--lines=N` | Output the last N lines (default: 10) |
| `-c`, `--bytes=N` | Output the last N bytes |

## Examples

```bash
# Show last 10 lines (default)
idlebox tail file.txt

# Show last 3 lines
idlebox tail -n 3 file.txt

# Show last 50 bytes
idlebox tail -c 50 file.txt

# Read from stdin pipe
echo -e "a\nb\nc\nd\ne" | idlebox tail -n 2
# Output: d, e

# Show headers when processing multiple files
idlebox tail -n 3 file1.txt file2.txt
# Output:
# ==> file1.txt <==
# ...
# ==> file2.txt <==
# ...
```

## Implementation Notes

- Located in `src/applets/tail.rs`
- Line mode uses a ring buffer (Vec) for memory-efficient tail reading
- Byte mode for files uses `seek` from end for O(1) positioning
- Byte mode for stdin reads all input then extracts the tail
- Multiple files produce `==> filename <==` headers
- With no FILE or when FILE is `-`, reads from stdin

## See Also

- [head](head.md) — for reading the beginning of files
- [cat](cat.md) — for reading entire files
- [Architecture Overview](../architecture.md)
