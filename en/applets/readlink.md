# readlink — Print Resolved Symbolic Links or Canonical File Names

> **Other languages:** [中文](../../zh/applets/readlink.md)

## Synopsis

```
readlink [OPTION]... FILE...
```

## Description

The `readlink` applet prints the target of a symbolic link. With the `-f` option, it recursively resolves all symlinks in the path and outputs the canonical absolute path.

## Options

| Option | Description |
|--------|-------------|
| `-f`, `-e`, `--canonicalize` | Canonicalize by following every symlink in every component, resolving to an absolute path |
| `-n`, `--no-newline` | Do not output the trailing newline character |

## Examples

```bash
# Read the target of a symbolic link
idlebox readlink /path/to/symlink

# Resolve to canonical absolute path
idlebox readlink -f /path/to/symlink

# Read without trailing newline
idlebox readlink -n /path/to/symlink

# Combine flags
idlebox readlink -fn /path/to/symlink
```

## Output

Without `-f`, prints the immediate symlink target (which may be a relative path).
With `-f`, prints the fully resolved absolute path with all symlinks expanded.

## Implementation Notes

- Located in `src/applets/readlink.rs`
- Uses `std::fs::read_link` for reading symlink targets
- Uses `std::fs::canonicalize` for full path resolution
- Supports combined short flags (e.g., `-fn`, `-ne`)
- Multiple files can be processed in a single invocation

## See Also

- [ln](ln.md) — create links between files
- [Architecture Overview](../architecture.md)
