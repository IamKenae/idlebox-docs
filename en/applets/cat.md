# cat — Concatenate Files and Print to Standard Output

> **Other languages:** [中文](../../zh/applets/cat.md)

## Synopsis

```
cat [-n] [-b] [-A|-e] [FILE...]
```

## Description

The `cat` applet reads files sequentially and writes their contents to standard output. If no file is specified, or if `-` is given, it reads from standard input (stdin), enabling pipeline usage.

## Options

| Option | Description |
|--------|-------------|
| `-n`   | Number all output lines |
| `-b`   | Number non-empty output lines only (overrides `-n`) |
| `-A`   | Equivalent to `-vET`: show non-printing characters, tabs as `^I`, and `$` at line ends |
| `-e`   | Equivalent to `-vE`: show non-printing characters and `$` at line ends |
| `--`   | End of options; remaining arguments treated as file paths |

## Examples

```bash
# Print a file
idlebox cat README.md

# Print with line numbers
idlebox cat -n src/main.rs

# Number only non-empty lines
idlebox cat -b src/main.rs

# Show invisible characters
idlebox cat -A config.txt

# Read from stdin (pipeline)
echo "hello" | idlebox cat
# Output: hello

# Concatenate multiple files
idlebox cat file1.txt file2.txt file3.txt
```

## Implementation Notes

- Located in `src/applets/cat.rs`
- Uses `BufReader` for efficient buffered I/O
- Supports reading from stdin when no file is specified or when `-` is passed
- The `-A` flag reveals tabs as `^I`, control characters as `^X`, and appends `$` to each line
- Line numbering uses a right-aligned 6-character wide counter with a tab separator

## See Also

- [echo](echo.md) — for simple text output
- [ls](ls.md) — for listing directory contents
- [Architecture Overview](../architecture.md)
