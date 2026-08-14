# touch — Update File Timestamps or Create Empty Files

> **Other languages:** [中文](../../zh/applets/touch.md)

## Synopsis

```
touch [OPTION]... FILE...
```

## Description

The `touch` applet creates empty files if they do not exist, or updates the access and modification timestamps of existing files to the current time.

## Arguments

| Argument | Description |
|----------|-------------|
| `FILE...` | One or more file paths to create or update |

## Examples

```bash
# Create a single empty file
idlebox touch newfile.txt

# Create multiple empty files at once
idlebox touch file1.txt file2.txt file3.txt

# Update timestamps of an existing file
idlebox touch existing.txt

# Create a file and use it immediately
idlebox touch log.txt
idlebox echo "started" >> log.txt
```

## Implementation Notes

- Located in `src/applets/touch.rs`
- Uses `std::fs::File::create` for new file creation
- On Unix systems, uses the `utimes` syscall to update timestamps
- Multiple files are processed sequentially; errors in one do not prevent others
- Returns exit code 1 if any operation fails

## See Also

- [cat](cat.md) — for reading file contents
- [head](head.md) — for reading the beginning of files
- [tail](tail.md) — for reading the end of files
- [Architecture Overview](../architecture.md)
