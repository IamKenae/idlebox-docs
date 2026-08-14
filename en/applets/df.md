# df — Report File System Disk Space Usage

> **Other languages:** [中文](../../zh/applets/df.md)

## Synopsis

```
df [-h] [FILE]
```

## Description

The `df` applet reports file system disk space usage. It reads mount information from `/proc/mounts` and queries each file system via the `statvfs` system call. Without arguments, it displays all mounted file systems. When a path is given, it shows information about the file system containing that path.

## Options

| Option | Description |
|--------|-------------|
| `-h`, `--human-readable` | Print sizes in human readable format (B, K, M, G, T) |

## Output Format

```
Filesystem                 Size       Used      Avail  Use%  Mounted on
/dev/sda1                 50.0G      20.0G      30.0G   40%  /
```

## Examples

```bash
# Show all file systems in human readable format
idlebox df -h

# Show disk usage for root directory
idlebox df -h /

# Show raw block counts for /tmp
idlebox df /tmp
```

## Implementation Notes

- Located in `src/applets/df.rs`
- Parses `/proc/mounts` for mount point information
- Uses the POSIX `statvfs` system call via FFI for disk space queries
- Filters out pseudo-filesystems (proc, sysfs, devtmpfs, etc.) when listing all mounts
- Handles octal-escaped paths in `/proc/mounts`

## See Also

- [du](du.md) — estimate file space usage
- [Architecture Overview](../architecture.md)
