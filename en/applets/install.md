# --install — Automated Applet Deployment

> **Other languages:** [中文](../../zh/applets/install.md)

## Synopsis

```
idlebox --install [OPTIONS] [PATH]
```

## Description

The `--install` command deploys every registered IdleBox applet by creating a platform-appropriate launcher in a target directory. Each launcher reuses the current `idlebox` binary under an applet-specific name. IdleBox reads that name from `argv[0]` and dispatches to the matching applet.

This is the recommended way to make IdleBox applets available system-wide or in a custom `PATH` directory.

| Platform | Launcher | Default target directory |
|----------|----------|--------------------------|
| Unix-like systems | Symbolic link | `/usr/local/bin` |
| Windows | `<applet>.exe` hard link, with a file-copy fallback | `%LOCALAPPDATA%\IdleBox\bin`; falls back to `%USERPROFILE%\.local\bin` |

## Arguments

| Argument or option | Description |
|--------------------|-------------|
| `[PATH]` | Optional target directory. When supplied, it overrides the platform default. |
| `--dry-run` | Preview every planned install, update, skip, and conflict without creating the target directory or changing launchers. |
| `--force` | Replace conflicting files and links. Directories are never replaced. |
| `-h`, `--help` | Print command-specific help. |

Use `--` before PATH when the path starts with `-`. More than one target path is rejected instead of being silently ignored, and `idlebox --install --help` prints command-specific help without installing anything.

## Behavior

- Gets the complete applet list from the dispatcher and checks every destination before writing anything.
- Creates the target directory if it does not exist, except during `--dry-run`.
- On Unix-like systems, creates symbolic links. A launcher in the same directory as `idlebox` uses a relative target; other launchers use the canonical binary path.
- On Windows, creates `<applet>.exe` hard links. If a hard link cannot be created, for example across filesystems, it falls back to an exclusive file copy.
- Skips launchers that already resolve to the current IdleBox binary. Byte-identical Windows copy launchers are also treated as current.
- Rejects unrelated existing files and links by default. If any conflict is found, preflight reports all conflicts and leaves every launcher unchanged.
- With `--force`, replaces conflicting files and links, but still rejects and preserves directories.
- Builds each installed or updated launcher at a temporary sibling path before moving it into place.
- Prints each install or update action, the installation method (`symbolic link`, `hard link`, or `copy`), a final summary including skipped launchers, and a `PATH` hint when needed. Dry runs list every planned action.
- Supports Unix-like systems and Windows. Other platforms return an unsupported-platform error.

## Examples

```bash
# Unix: install to the default location
idlebox --install
# Output:
# Installing IdleBox applets to /usr/local/bin...
#   Installed: /usr/local/bin/cat (symbolic link)
#   Installed: /usr/local/bin/echo (symbolic link)
#   ...
# Done. 52 installed, 0 updated, 0 already installed.

# Install to a custom directory
idlebox --install ./bin

# Preview an installation without creating ./bin or changing launchers
idlebox --install --dry-run ./bin

# Explicitly replace conflicting files or links
idlebox --install --force ./bin

# Install to a path whose name starts with a dash
idlebox --install -- -tools

# Use the installed applets directly
./bin/echo "hello from a launcher"
./bin/ls -lah
```

On Windows PowerShell:

```powershell
# Install to %LOCALAPPDATA%\IdleBox\bin
.\idlebox.exe --install
# Output:
# Installing IdleBox applets to C:\Users\me\AppData\Local\IdleBox\bin...
#   Installed: C:\Users\me\AppData\Local\IdleBox\bin\cat.exe (hard link)
#   ...
# Done. 52 installed, 0 updated, 0 already installed.

# Install to and invoke from a custom directory
.\idlebox.exe --install .\bin
.\bin\echo.exe "hello from a launcher"
```

## Notes

- A Windows hard-link launcher shares the same file data as the current `idlebox.exe`, while a copy fallback is an independent snapshot. After replacing the original binary, rerun with `--force` if the old copies are reported as conflicts.
- Rerunning `--install` is idempotent: current launchers are skipped. Use `--force` only when you intend to replace a different or outdated file or link.
- Preflight avoids predictable partial installations caused by existing-path conflicts. A later filesystem or permission error can still stop an installation after earlier launchers were written; each individual replacement remains staged and recoverable.
- After installation, ensure the target directory is in your `PATH` environment variable to invoke applets by name.
- To uninstall, remove the launchers from the target directory.

## See Also

- [Architecture Overview](../architecture.md)
- [echo](echo.md) · [cat](cat.md) · [ls](ls.md) · [relax](relax.md)
