# free — Display Memory Usage

> **Other languages:** [中文](../../zh/applets/free.md)

## Synopsis

```
free [-h]
```

## Description

The `free` applet displays the total amount of free and available physical memory and swap space, as well as the buffers and cache used by the kernel. It reads data from `/proc/meminfo`.

## Options

| Option | Description |
|--------|-------------|
| `-h`, `--human-readable` | Print sizes in human readable format (B, K, M, G, T) |

## Output Format

```
              total        used        free      shared   buff/cache   available
Mem:        8048564     4123456     1234567      234567     2690541     3654321
Swap:       2097148      123456     1973692
```

With `-h`:

```
              total        used        free      shared   buff/cache   available
Mem:           7.7G        3.9G        1.2G       229M        2.6G        3.5G
Swap:          2.0G       120.6M        1.9G
```

## Examples

```bash
# Show memory usage in kilobytes
idlebox free

# Show memory usage in human readable format
idlebox free -h
```

## Implementation Notes

- Located in `src/applets/free.rs`
- Parses `/proc/meminfo` for memory statistics
- Reads: MemTotal, MemFree, MemAvailable, Shmem, Buffers, Cached, SwapTotal, SwapFree
- Values in `/proc/meminfo` are in kilobytes (kB)
- Human-readable format uses binary units (1K = 1024 bytes)

## See Also

- [df](df.md) — report file system disk space usage
- [Architecture Overview](../architecture.md)
