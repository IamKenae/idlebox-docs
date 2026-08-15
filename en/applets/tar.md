# tar — Create, List, and Extract Archives

> **Other languages:** [中文](../../zh/applets/tar.md)

## Synopsis

```
tar (-c|-x|-t) [-zv] [-f ARCHIVE] [-C DIR] [FILE]...
```

## Description

`tar` reads and writes 512-byte POSIX ustar records. It recursively archives regular files and directories and preserves symbolic links without following them. Archive data may be passed through the pure-Rust Gzip backend with `-z`.

Exactly one operation mode is required. If `-f` is omitted, the archive is written to standard output in create mode or read from standard input in list/extract mode. `-` is also accepted explicitly as the archive name.

## Options

| Option | Description |
|--------|-------------|
| `-c`, `--create` | Create a new archive |
| `-x`, `--extract` | Extract archive members |
| `-t`, `--list` | Print member names without extracting |
| `-f`, `--file ARCHIVE` | Read or write `ARCHIVE` |
| `-z`, `--gzip` | Compress or decompress the tar stream as Gzip |
| `-C`, `--directory DIR` | Use `DIR` as the create base or extraction destination |
| `-v`, `--verbose` | Print members while creating or extracting |

Short options may be clustered; `-czvf archive.tar.gz files` is equivalent to separate `-c -z -v -f` options.

## Examples

```bash
idlebox tar -cvf source.tar src README.md
idlebox tar -tf source.tar
idlebox tar -xvf source.tar -C restored
idlebox tar -czf source.tar.gz src
idlebox tar -tzf source.tar.gz
```

## Safety and Format Notes

- Header checksums and octal numeric fields are validated before use.
- Regular-file payloads are staged and published only after the complete member has been read.
- File-backed archive creation is staged, so a failed create does not replace an existing archive.
- Unix file and directory permission bits are restored; restrictive directory modes are applied after their children are extracted.
- Absolute paths, Windows drive paths, backslash paths, and `..` components are rejected during extraction.
- Extraction refuses to traverse or overwrite symbolic links in the destination path.
- Symlink targets that could leave the extraction root are rejected.
- POSIX ustar regular files, directories, and symbolic links are supported. GNU/PAX extensions, device nodes, hard-link records, sparse files, and names beyond the ustar prefix/name limits are not currently supported.
- Symbolic-link creation is available on Unix-like systems; archives containing symlinks report an unsupported operation on other platforms.

## See Also

- [gzip](gzip.md)
- [gunzip](gunzip.md)
- [unzip](unzip.md)
