# md5sum

> **Other languages:** [中文](../../zh/applets/md5sum.md)
Compute and check MD5 message digest.

## Usage

```bash
idlebox md5sum [OPTION]... [FILE]...
```

## Options

* `-c, --check`: read MD5 sums from the FILEs and check them
* `-b, --binary`: read in binary mode
* `-t, --text`: read in text mode (default)
* `--status`: don't output anything, status code shows success

## Examples

Compute the MD5 hash of a file:
```bash
idlebox md5sum file.txt
```

Check the MD5 hash of files listed in a checksum file:
```bash
idlebox md5sum -c checksums.md5
```
