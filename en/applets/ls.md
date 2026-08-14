# ls — List Directory Contents

> **Other languages:** [中文](../../zh/applets/ls.md)

## Synopsis

```
ls [-a] [-l] [-h] [--color[=WHEN]] [PATH...]
```

## Description

The `ls` applet lists the contents of directories. It is one of the most feature-rich applets in IdleBox, with full support for ANSI colorized output that makes terminal navigation a visual pleasure.

## Options

| Option | Description |
|--------|-------------|
| `-a`, `--all` | Show all entries, including hidden files (starting with `.`) |
| `-l` | Use long listing format (permissions, owner, size, date) |
| `-h`, `--human-readable` | With `-l`, print sizes in human-readable format (e.g., `1.2K`, `3.4M`) |
| `--color` | Colorize output (equivalent to `--color=always`) |
| `--color=auto` | Colorize only when output is a terminal (TTY) |
| `--color=always` | Always colorize output |
| `--color=never` | Never colorize output |

Options can be combined in short form: `-la`, `-lh`, `-lah`, etc.

## Color Scheme

When color is enabled, `ls` uses the following ANSI color scheme:

| Type | Color | Code |
|------|-------|------|
| Directories | **Bold Blue** | `1;34` |
| Symbolic links | **Bold Cyan** | `1;36` |
| Executable files | **Bold Green** | `1;32` |
| Archives (`.tar`, `.gz`, `.zip`, etc.) | **Bold Red** | `1;31` |
| Regular files | Default | — |

## Examples

```bash
# Basic listing
idlebox ls

# Show hidden files
idlebox ls -a

# Long format
idlebox ls -l

# Long format with human-readable sizes
idlebox ls -lh

# Colorized output
idlebox ls --color=auto

# All options combined
idlebox ls -lah --color=auto

# List specific paths
idlebox ls /usr/bin /usr/local/bin
```

## Long Format Output

The `-l` flag produces output in the following format:

```
-rw-r--r--   1  1000  1000     1234 Aug 15 10:30 README.md
drwxr-xr-x   3  1000  1000     4096 Aug 14 09:00 src
-rwxr-xr-x   1  1000  1000   362K Aug 15 01:55 idlebox
```

Fields: `type+permissions`, `link count`, `UID`, `GID`, `size`, `modification date`, `filename`

## Implementation Notes

- Located in `src/applets/ls.rs`
- TTY detection uses raw `fstat` syscall (no libc dependency) to auto-detect color support
- Human-readable sizes use binary units (1K = 1024 bytes)
- Timestamps are formatted using a custom date calculation (no chrono dependency)
- Permission bits include SUID/SGID/sticky bit indicators (`s`, `S`, `t`, `T`)
- Entries are sorted alphabetically by filename

## See Also

- [cat](cat.md) — for reading file contents
- [Architecture Overview](../architecture.md)
