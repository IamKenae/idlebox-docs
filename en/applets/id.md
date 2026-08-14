# id — Print Real and Effective User and Group IDs

> **Other languages:** [中文](../../zh/applets/id.md)

## Synopsis

```
id [OPTION]... [USER]
```

## Description

The `id` applet prints the real and effective user ID and group ID of the current user, or of a specified user. With no options, it prints the UID, GID, and supplementary group list.

## Options

| Option | Description |
|--------|-------------|
| `-u`, `--user` | Print only the effective user ID |
| `-g`, `--group` | Print only the effective group ID |
| `-G`, `--groups` | Print all supplementary group IDs |
| `-n`, `--name` | Print a name instead of a number (requires `-u`, `-g`, or `-G`) |

## Examples

```bash
# Print full identity information
idlebox id

# Print only the effective UID
idlebox id -u

# Print the effective user name
idlebox id -u -n

# Print only the effective GID
idlebox id -g

# Print all group IDs
idlebox id -G

# Query a specific user
idlebox id root
```

## Implementation Notes

- Located in `src/applets/id.rs`
- Uses POSIX `getuid()`, `geteuid()`, `getgid()`, `getegid()`, `getpwuid()`, `getpwnam()`, `getgrgid()`, `getgroups()`, and `getgrouplist()` FFI calls
- Zero external dependencies — pure Rust standard library + POSIX libc FFI
- Default output format: `uid=1000(username) gid=1000(groupname) groups=1000(groupname),...`

## See Also

- [whoami](whoami.md) — print effective user name
- [su](su.md) — switch user
- [Architecture Overview](../architecture.md)
