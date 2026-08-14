# --install — Automated Applet Deployment

> **Other languages:** [中文](../../zh/applets/install.md)

## Synopsis

```
idlebox --install [PATH]
```

## Description

The `--install` command automates the deployment of all registered IdleBox applets by creating symbolic links (symlinks) in a target directory. Each symlink points back to the current `idlebox` binary, enabling the multi-call binary pattern — invoking the binary via a symlink name automatically dispatches to the corresponding applet.

This is the recommended way to make IdleBox applets available system-wide or in a custom `PATH` directory.

## Arguments

| Argument | Description |
|----------|-------------|
| `[PATH]` | Target directory for symlinks. Defaults to `/usr/local/bin` if omitted. |

## Behavior

- Creates the target directory if it does not exist.
- Iterates over all registered applets (`cat`, `echo`, `ls`, `relax`).
- Creates a symlink for each applet pointing to the running `idlebox` binary.
- Overwrites any existing file or symlink at the destination without prompting.
- Uses `std::os::unix::fs::symlink` — only supported on Unix-like systems (Linux, macOS, BSD). On other platforms, an error message is printed.

## Examples

```bash
# Install to the default location (/usr/local/bin)
idlebox --install
# Output:
# Installing IdleBox applets to /usr/local/bin...
#   Created symlink: /usr/local/bin/cat -> idlebox
#   Created symlink: /usr/local/bin/echo -> idlebox
#   Created symlink: /usr/local/bin/ls -> idlebox
#   Created symlink: /usr/local/bin/relax -> idlebox
# Done. 4 applets installed.

# Install to a custom directory
idlebox --install /tmp/mybin
# Output:
# Installing IdleBox applets to /tmp/mybin...
#   Created symlink: /tmp/mybin/cat -> idlebox
#   ...

# Use the installed applets directly
echo "hello" | /tmp/mybin/cat
/tmp/mybin/ls -lah /tmp
```

## Notes

- The symlinks use the canonical (absolute) path to the `idlebox` binary when the target directory differs from the binary's own directory. When installing to the same directory as the binary, relative symlinks are created.
- After installation, ensure the target directory is in your `$PATH` to invoke applets by name.
- To uninstall, simply remove the symlinks from the target directory.

## See Also

- [Architecture Overview](../architecture.md)
- [echo](echo.md) · [cat](cat.md) · [ls](ls.md) · [relax](relax.md)
