# head — Output the First Part of Files

> **Other languages:** [中文](../../zh/applets/head.md)

## Synopsis

```
head [OPTION]... [FILE]...
```

## Description

The `head` applet outputs the first part of files. By default, it prints the first 10 lines of each file. With no file, or when the file is `-`, it reads from standard input.

## Options

| Option | Description |
|--------|-------------|
| `-n`, `--lines=N` | Output the first N lines (default: 10) |
| `-c`, `--bytes=N` | Output the first N bytes |

## Examples

```bash
# Show first 10 lines (default)
idlebox head file.txt

# Show first 5 lines
idlebox head -n 5 file.txt

# Show first 100 bytes
idlebox head -c 100 file.txt

# Read from stdin pipe
echo -e "a\nb\nc\nd\ne" | idlebox head -n 3
# Output: a, b, c

# Show headers when processing multiple files
idlebox head -n 3 file1.txt file2.txt
# Output:
# ==> file1.txt <==
# ...
# ==> file2.txt <==
# ...
```

## Implementation Notes

- Located in `src/applets/head.rs`
- Uses `BufReader` for efficient line-by-line reading
- Byte mode uses a streaming approach with an 8KB buffer
- Multiple files produce `==> filename <==` headers
- With no FILE or when FILE is `-`, reads from stdin

## See Also

- [tail](tail.md) — for reading the end of files
- [cat](cat.md) — for reading entire files
- [Architecture Overview](../architecture.md)
