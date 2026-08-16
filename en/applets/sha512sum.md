# sha512sum

> **Other languages:** [中文](../../zh/applets/sha512sum.md)
Compute and check SHA512 message digest.

## Usage

```bash
idlebox sha512sum [OPTION]... [FILE]...
```

## Options

* `-c, --check`: read SHA512 sums from the FILEs and check them
* `-b, --binary`: read in binary mode
* `-t, --text`: read in text mode (default)
* `--status`: don't output anything, status code shows success

## Examples

Compute the SHA512 hash of a file:
```bash
idlebox sha512sum file.txt
```

Check the SHA512 hash of files listed in a checksum file:
```bash
idlebox sha512sum -c checksums.sha512
```
