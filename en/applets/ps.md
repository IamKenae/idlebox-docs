# ps — Report a Snapshot of Current Processes

> **Other languages:** [中文](../../zh/applets/ps.md)

## Synopsis

```
ps [-e] [-A] [-o COL1,COL2,...]
```

## Description

The `ps` applet displays a snapshot of currently running processes. It reads process information from the `/proc` filesystem, parsing `/proc/[pid]/stat` and `/proc/[pid]/cmdline` for each process.

## Options

| Option | Description |
|--------|-------------|
| `-e`, `-A` | Show all processes (default shows only current session) |
| `-o COL1,COL2,...` | Custom output columns |

### Available Columns

| Column | Description |
|--------|-------------|
| `pid` | Process ID |
| `tty` | Controlling terminal |
| `stat` | Process state (R=running, S=sleeping, Z=zombie, etc.) |
| `time` | Cumulative CPU time |
| `cmd` | Command with all arguments |

## Output Format

```
     PID TTY      STAT       TIME COMMAND
       1 ?        S        00:03 /sbin/init
     123 pts/0    S        00:00 bash
```

## Examples

```bash
# Show all processes
idlebox ps -e

# Show only current session processes
idlebox ps

# Custom columns: PID and command only
idlebox ps -e -o pid,cmd
```

## Implementation Notes

- Located in `src/applets/ps.rs`
- Parses `/proc/[pid]/stat` for process state, TTY, and CPU time
- Parses `/proc/[pid]/cmdline` for the full command line
- Gracefully handles processes that vanish during enumeration (ENOENT)
- Gracefully handles permission-denied errors on restricted `/proc` entries

## See Also

- [kill](kill.md) — send signals to processes
- [Architecture Overview](../architecture.md)
