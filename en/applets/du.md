# du — Estimate File Space Usage

> **Other languages:** [中文](../../zh/applets/du.md)

## Synopsis

```
du [-h] [-s] [-d N] [FILE]...
```

## Description

The `du` applet estimates file and directory space usage by recursively summing the disk blocks consumed by each entry. Sizes are reported based on actual disk block usage (via `MetadataExt::blocks`), not logical file size.

## Options

| Option | Description |
|--------|-------------|
| `-h`, `--human-readable` | Print sizes in human readable format (B, K, M, G, T) |
| `-s`, `--summarize` | Display only a total for each argument |
| `-d N`, `--max-depth N` | Print total for a directory only if it is N or fewer levels below the argument |

## Examples

```bash
# Show disk usage of current directory
idlebox du

# Show total only for /var/log
idlebox du -s /var/log

# Human readable sizes with max depth of 1
idlebox du -h -d 1 /home

# Human readable summary
idlebox du -h -s /tmp
```

## Implementation Notes

- Located in `src/applets/du.rs`
- Uses `std::os::unix::fs::MetadataExt::blocks()` to get actual disk block usage
- Block sizes are calculated as `blocks * 512` bytes (POSIX standard)
- Defaults to current directory when no path is given
- `-d 0` is equivalent to `-s`

## See Also

- [df](df.md) — report file system disk space usage
- [ls](ls.md) — list directory contents with sizes
- [Architecture Overview](../architecture.md)
