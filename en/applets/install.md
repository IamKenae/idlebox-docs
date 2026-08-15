# --install — Automated Applet Deployment

> **Other languages:** [中文](../../zh/applets/install.md)

## Synopsis

```
idlebox --install [PATH]
```

## Description

The `--install` command deploys every registered IdleBox applet by creating a platform-appropriate launcher in a target directory. Each launcher reuses the current `idlebox` binary under an applet-specific name. IdleBox reads that name from `argv[0]` and dispatches to the matching applet.

This is the recommended way to make IdleBox applets available system-wide or in a custom `PATH` directory.

| Platform | Launcher | Default target directory |
|----------|----------|--------------------------|
| Unix-like systems | Symbolic link | `/usr/local/bin` |
| Windows | `<applet>.exe` hard link, with a file-copy fallback | `%LOCALAPPDATA%\IdleBox\bin`; falls back to `%USERPROFILE%\.local\bin` |

## Arguments

| Argument | Description |
|----------|-------------|
| `[PATH]` | Optional target directory. When supplied, it overrides the platform default. |

Use `--` before PATH when the path starts with `-`. More than one target path is rejected instead of being silently ignored, and `idlebox --install --help` prints command-specific help without installing anything.

## Behavior

- Creates the target directory if it does not exist.
- Gets the complete applet list from the dispatcher and creates one launcher per registered name.
- On Unix-like systems, creates symbolic links. A launcher in the same directory as `idlebox` uses a relative target; other launchers use the canonical binary path.
- On Windows, creates `<applet>.exe` hard links. If a hard link cannot be created, for example across filesystems, it falls back to an exclusive file copy.
- Builds each replacement at a temporary sibling path before moving it into place. Existing files and launchers are replaced without prompting, but existing directories are rejected and preserved.
- Prints the installation method (`symbolic link`, `hard link`, or `copy`) for each launcher.
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
# Done. 36 applets installed.

# Install to a custom directory
idlebox --install ./bin

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
# Done. 36 applets installed.

# Install to and invoke from a custom directory
.\idlebox.exe --install .\bin
.\bin\echo.exe "hello from a launcher"
```

## Notes

- A Windows hard-link launcher shares the same file data as the current `idlebox.exe`, while a copy fallback is an independent snapshot. Rerun `--install` after replacing the original binary to ensure every launcher is refreshed.
- Rerunning `--install` refreshes existing launchers. It never removes a directory that conflicts with a launcher name.
- After installation, ensure the target directory is in your `PATH` environment variable to invoke applets by name.
- To uninstall, remove the launchers from the target directory.

## See Also

- [Architecture Overview](../architecture.md)
- [echo](echo.md) · [cat](cat.md) · [ls](ls.md) · [relax](relax.md)
