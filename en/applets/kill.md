# kill — Send Signals to Processes

> **Other languages:** [中文](../../zh/applets/kill.md)

## Synopsis

```
kill [-SIGNAL] PID...
kill -s SIGNAL PID...
kill -l
```

## Description

The `kill` applet sends POSIX signals to specified processes. Signals can be specified by number (e.g., `-9`) or by name (e.g., `-TERM`, `-KILL`, `-HUP`). The default signal is `SIGTERM` (15).

## Options

| Option | Description |
|--------|-------------|
| `-SIGNAL` | Signal number or name (e.g., `-9`, `-TERM`, `-KILL`) |
| `-s SIGNAL` | Specify signal by number or name |
| `-l`, `--list` | List all available signals with their numbers |

## Supported Signals

| Number | Name | Description |
|--------|------|-------------|
| 1 | HUP | Hangup |
| 2 | INT | Interrupt (Ctrl+C) |
| 3 | QUIT | Quit |
| 9 | KILL | Kill (cannot be caught) |
| 15 | TERM | Terminate (default) |
| 17 | CHLD | Child process status changed |
| 18 | CONT | Continue |
| 19 | STOP | Stop (cannot be caught) |
| 20 | TSTP | Terminal stop |

## Examples

```bash
# Send SIGTERM (default) to PID 1234
idlebox kill 1234

# Send SIGKILL to PID 1234
idlebox kill -9 1234

# Send SIGKILL by name
idlebox kill -KILL 1234

# Send signal using -s option
idlebox kill -s TERM 1234 5678

# List all available signals
idlebox kill -l
```

## Implementation Notes

- Located in `src/applets/kill.rs`
- Uses POSIX `kill(pid, sig)` system call via FFI
- Supports all 31 standard POSIX signals (1-31)
- Signal names are case-insensitive and may optionally include the `SIG` prefix

## See Also

- [ps](ps.md) — report process status
- [Architecture Overview](../architecture.md)
