# ln — Create Links Between Files

> **Other languages:** [中文](../../zh/applets/ln.md)

## Synopsis

```
ln [OPTION]... TARGET LINK_NAME
ln [OPTION]... TARGET... DIRECTORY
```

## Description

The `ln` applet creates links between files. By default, it creates hard links. With the `-s` option, it creates symbolic (soft) links.

A hard link is a directory entry that points to the same inode as the original file. A symbolic link is a special file that contains a path reference to another file.

## Options

| Option | Description |
|--------|-------------|
| `-s`, `--symbolic` | Create a symbolic link instead of a hard link |
| `-f`, `--force` | Remove existing destination files before creating the link |

## Examples

```bash
# Create a symbolic link
idlebox ln -s /path/to/target /path/to/link

# Create a hard link
idlebox ln /path/to/target /path/to/link

# Force overwrite an existing link
idlebox ln -sf /path/to/target /path/to/existing_link

# Create symbolic links for multiple files in a directory
idlebox ln -s file1.txt file2.txt /path/to/directory/
```

## Implementation Notes

- Located in `src/applets/ln.rs`
- Uses `std::os::unix::fs::symlink` for symbolic links
- Uses `std::fs::hard_link` for hard links
- Supports combined short flags (e.g., `-sf`)
- When linking multiple files to a directory, the link name is derived from the source file name

## See Also

- [readlink](readlink.md) — print resolved symbolic links
- [Architecture Overview](../architecture.md)
