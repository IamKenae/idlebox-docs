# sha256sum

Compute and check SHA256 message digest.

## Usage

```bash
idlebox sha256sum [OPTION]... [FILE]...
```

## Options

* `-c, --check`: read SHA256 sums from the FILEs and check them
* `-b, --binary`: read in binary mode
* `-t, --text`: read in text mode (default)
* `--status`: don't output anything, status code shows success

## Examples

Compute the SHA256 hash of a file:
```bash
idlebox sha256sum file.txt
```

Check the SHA256 hash of files listed in a checksum file:
```bash
idlebox sha256sum -c checksums.sha256
```
