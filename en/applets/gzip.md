# gzip — Compress or Decompress Gzip Data

> **Other languages:** [中文](../../zh/applets/gzip.md)

## Synopsis

```
gzip [OPTION]... [FILE]...
```

## Description

`gzip` writes RFC 1952 Gzip streams using the pure-Rust `miniz_oxide` backend. With no file, or with `-`, it reads standard input and writes standard output.

For file operands, compression writes `FILE.gz`; decompression removes `.gz`, or maps `.tgz` to `.tar`. A successful file operation removes its input unless `-k` is used. Writing to standard output never removes an input file.

## Options

| Option | Description |
|--------|-------------|
| `-d`, `--decompress` | Decompress instead of compressing |
| `-k`, `--keep` | Keep input files after successful output |
| `-f`, `--force` | Replace an existing output file |
| `-c`, `--to-stdout` | Write the result to standard output |

Short options may be combined, for example `-dc` or `-kf`.

## Examples

```bash
idlebox gzip report.txt
idlebox gzip -k archive.tar
idlebox gzip -dc report.txt.gz > report.txt
idlebox cat payload.bin | idlebox gzip -c > payload.bin.gz
```

## Safety and Implementation Notes

- Compression and decompression are streamed rather than buffering the complete file.
- File output is written to a temporary file in the destination directory and published only after the stream succeeds.
- Source-file permissions are applied to the staged output before it is published.
- Existing destinations are protected unless `-f` is explicit.
- Multi-member Gzip input is supported and checksums are validated by the decoder.
- `flate2` is built with `default-features = false` and the pure-Rust `rust_backend`; no zlib C library is linked.

## See Also

- [gunzip](gunzip.md)
- [zcat](zcat.md)
- [tar](tar.md)
