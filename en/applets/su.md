# su — Switch User

> **Other languages:** [中文](../../zh/applets/su.md)

## Synopsis

```
su [options] [USER]
```

## Description

The `su` applet allows running a shell with substitute user and group IDs. If no user is specified, it defaults to `root`. **Note: only root can switch to another user.**

## Options

| Option | Description |
|--------|-------------|
| `-`, `-l`, `--login` | Make the shell a login shell (reset environment variables) |
| `-c`, `--command` | Pass a command to the shell to execute |
| `-s`, `--shell` | Use the specified shell instead of the user's default |

## Examples

```bash
# Switch to root (requires root privileges)
idlebox su

# Switch to a specific user
idlebox su username

# Execute a single command as another user
idlebox su -c "whoami" root

# Login shell simulation
idlebox su -l username

# Use a specific shell
idlebox su -s /bin/bash username
```

## Implementation Notes

- Located in `src/applets/su.rs`
- Uses POSIX `getpwnam()` and `getuid()` FFI calls
- Login shell mode resets `HOME`, `USER`, `SHELL`, `LOGNAME`, and `PATH`
- Only root (UID 0) can switch to another user; non-root users will receive a permission denied error
- Zero external dependencies — pure Rust standard library + POSIX libc FFI

## See Also

- [id](id.md) — print user and group IDs
- [whoami](whoami.md) — print effective user name
- [Architecture Overview](../architecture.md)
