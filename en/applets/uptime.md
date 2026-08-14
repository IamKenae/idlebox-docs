# uptime — Tell How Long the System Has Been Running

> **Other languages:** [中文](../../zh/applets/uptime.md)

## Synopsis

```
uptime
```

## Description

The `uptime` applet displays the current time, how long the system has been running, the number of users, and the system load averages for the past 1, 5, and 15 minutes. It reads data from `/proc/uptime` and `/proc/loadavg`.

## Options

This applet takes no options.

## Output Format

```
2024-01-15 14:30:22  up 5 days, 03:42,  1 user,  load average: 0.15, 0.20, 0.18
```

## Examples

```bash
# Show system uptime and load average
idlebox uptime
```

## Output Fields

| Field | Description |
|-------|-------------|
| Current time | System date and time (YYYY-MM-DD HH:MM:SS) |
| up X days, HH:MM | System uptime since last boot |
| 1 user | Number of logged-in users (simplified, defaults to 1) |
| load average | 1, 5, and 15 minute system load averages |

## Implementation Notes

- Located in `src/applets/uptime.rs`
- Parses `/proc/uptime` for system uptime in seconds
- Parses `/proc/loadavg` for 1/5/15 minute load averages and task counts
- Uses `gettimeofday` system call via FFI for current time
- Computes calendar date from Unix epoch days without external date libraries

## See Also

- [ps](ps.md) — report process status
- [Architecture Overview](../architecture.md)
