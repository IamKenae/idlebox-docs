# zcat — Decompress Gzip Data to Standard Output

> **Other languages:** [中文](../../zh/applets/zcat.md)

## Synopsis

```
zcat [FILE]...
```

## Description

`zcat` decompresses every named Gzip file to standard output without changing or deleting the source. With no file, or with `-`, it reads a Gzip stream from standard input. It is equivalent to the common `gzip -dc` workflow.

## Examples

```bash
idlebox zcat server.log.gz
idlebox zcat part-1.gz part-2.gz > combined.txt
idlebox cat payload.gz | idlebox zcat
```

## Terminal Behavior

When standard input is a terminal, `zcat` prints an error and exits rather than blocking. Pipe data from another command to decompress from standard input.

## See Also

- [gzip](gzip.md)
- [gunzip](gunzip.md)
- [cat](cat.md)
