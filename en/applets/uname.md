# uname — Print System Information

> **Other languages:** [中文](../../zh/applets/uname.md)

## Synopsis

```
uname [OPTION]...
```

## Description

The `uname` applet prints system information obtained from the POSIX `uname()` system call. Without any options, it prints the kernel name (equivalent to `-s`).

## Options

| Option | Description |
|--------|-------------|
| `-a`, `--all` | Print all information |
| `-s`, `--sysname` | Print the kernel name (e.g., Linux) |
| `-n`, `--nodename` | Print the network node hostname |
| `-r`, `--release` | Print the kernel release (e.g., 5.15.0-generic) |
| `-v`, `--version` | Print the kernel version |
| `-m`, `--machine` | Print the machine hardware name (e.g., x86_64) |

## Examples

```bash
# Print kernel name (default)
idlebox uname

# Print all system information
idlebox uname -a

# Print kernel release
idlebox uname -r

# Print machine architecture
idlebox uname -m

# Combine multiple flags
idlebox uname -sm
```

## Output Format

```
# uname -a
Linux myhost 5.15.0-generic #1 SMP Fri Jan 1 00:00:00 UTC 2024 x86_64
```

## Implementation Notes

- Located in `src/applets/uname.rs`
- Uses POSIX `uname()` system call via FFI
- Parses the `utsname` structure returned by the kernel
- Supports combined short flags (e.g., `-sm`, `-rn`)
- Fields are printed in a fixed order: sysname, nodename, release, version, machine

## See Also

- [uptime](uptime.md) — tell how long the system has been running
- [Architecture Overview](../architecture.md)
