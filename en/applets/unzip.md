# unzip — List and Extract ZIP Archives

> **Other languages:** [中文](../../zh/applets/unzip.md)

## Synopsis

```
unzip [OPTION]... ARCHIVE
```

## Description

`unzip` reads the ZIP central directory, lists its entries, or safely extracts them. Stored entries and raw-Deflate entries are supported. The implementation uses the pure-Rust DEFLATE backend and validates each extracted file's declared size and CRC32.

## Options

| Option | Description |
|--------|-------------|
| `-l`, `--list` | List entries without extracting |
| `-o`, `--overwrite` | Replace existing regular files |
| `-d DIR`, `--directory DIR` | Extract under `DIR` instead of the current directory |

Options may appear before or after the archive operand. Use `--` before an archive name beginning with `-`.

## Examples

```bash
idlebox unzip -l release.zip
idlebox unzip release.zip -d release
idlebox unzip -o release.zip -d release
```

## Safety and Format Notes

- Both local headers and the central directory are bounds-checked and cross-checked.
- CRC32 and uncompressed sizes are checked before a staged replacement is published; an incomplete new file is removed if validation fails.
- On Unix-like systems, permission bits recorded by Unix ZIP writers are restored; restrictive directory modes are applied after their children are extracted.
- Absolute paths, drive-prefixed names, NULs, and `..` components are rejected to prevent Zip Slip.
- Extraction refuses to traverse or replace symbolic links and refuses special-file entries.
- Existing files are protected by default. `-o` decodes to a sibling temporary file before performing the replacement.
- Data-descriptor entries, UTF-8 names, and legacy CP437 names are supported.
- Encrypted archives, ZIP64, multi-disk archives, and compression methods other than Stored (0) and Deflate (8) are reported as unsupported.

## See Also

- [tar](tar.md)
- [gzip](gzip.md)
