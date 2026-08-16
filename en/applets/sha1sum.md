# sha1sum

Compute and check SHA1 message digest.

## Usage

```bash
idlebox sha1sum [OPTION]... [FILE]...
```

## Options

* `-c, --check`: read SHA1 sums from the FILEs and check them
* `-b, --binary`: read in binary mode
* `-t, --text`: read in text mode (default)
* `--status`: don't output anything, status code shows success

## Examples

Compute the SHA1 hash of a file:
```bash
idlebox sha1sum file.txt
```

Check the SHA1 hash of files listed in a checksum file:
```bash
idlebox sha1sum -c checksums.sha1
```
