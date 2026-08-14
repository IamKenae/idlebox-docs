# echo — Print Text to Standard Output

> **Other languages:** [中文](../../zh/applets/echo.md)

## Synopsis

```
echo [-n] [STRING...]
```

## Description

The `echo` applet writes its arguments to standard output, separated by spaces, followed by a newline. It is one of the simplest applets in IdleBox.

## Options

| Option | Description |
|--------|-------------|
| `-n`   | Do not output the trailing newline |

## Examples

```bash
# Basic usage
idlebox echo "Hello, World!"
# Output: Hello, World!

# Multiple arguments (joined with spaces)
idlebox echo Hello World
# Output: Hello World

# Suppress trailing newline
idlebox echo -n "no newline here"
# Output: no newline here (cursor stays on same line)
```

## Implementation Notes

- Located in `src/applets/echo.rs`
- Uses `println!` / `print!` macros from the Rust standard library
- Arguments are joined with a single space character
- The `-n` flag must be the first argument to take effect

## See Also

- [cat](cat.md) — for reading file contents
- [Architecture Overview](../architecture.md)
