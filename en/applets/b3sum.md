# b3sum

> **Other languages:** [中文](../../zh/applets/b3sum.md)
Compute and check BLAKE3 message digest (optimized for high speed and parallel hashing on large files).

## Usage

```bash
idlebox b3sum [OPTION]... [FILE]...
```

## Options

* `-c, --check`: read BLAKE3 sums from the FILEs and check them
* `-b, --binary`: read in binary mode
* `-t, --text`: read in text mode (default)
* `--status`: don't output anything, status code shows success

## Examples

Compute the BLAKE3 hash of a large file (automatically parallelized):
```bash
idlebox b3sum big_file.iso
```

Check the BLAKE3 hash of files listed in a checksum file:
```bash
idlebox b3sum -c checksums.b3
```
