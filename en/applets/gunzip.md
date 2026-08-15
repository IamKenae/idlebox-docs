# gunzip — Decompress Gzip Files

> **Other languages:** [中文](../../zh/applets/gunzip.md)

## Synopsis

```
gunzip [OPTION]... [FILE]...
```

## Description

`gunzip` is the decompression-oriented interface to the same streaming engine as `gzip -d`. `.gz` is removed from output names and `.tgz` becomes `.tar`. With no file, or with `-`, compressed data is read from standard input and plain data is written to standard output.

## Options

| Option | Description |
|--------|-------------|
| `-k`, `--keep` | Keep compressed input files |
| `-f`, `--force` | Replace an existing output file |
| `-c`, `--to-stdout` | Write decompressed data to standard output |

## Examples

```bash
idlebox gunzip archive.tar.gz
idlebox gunzip -k report.txt.gz
idlebox gunzip -c image.raw.gz > image.raw
```

The failure-safe output and pure-Rust backend guarantees documented for [gzip](gzip.md) also apply to `gunzip`.

## Terminal Behavior

When standard input is a terminal, `gunzip` prints an error and exits rather than blocking. Use `-f` to force decompression, or pipe data from another command.

## See Also

- [gzip](gzip.md)
- [zcat](zcat.md)
