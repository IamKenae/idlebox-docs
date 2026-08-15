# tee — Copy Standard Input to Files and Standard Output

> **Other languages:** [中文](../../zh/applets/tee.md)

## Synopsis

```
tee [OPTION]... [FILE]...
```

## Description

`tee` reads standard input once and copies each chunk to standard output and every named file.

## Options

| Option | Description |
|--------|-------------|
| `-a`, `--append` | Append instead of replacing file contents |
| `-i`, `--ignore-interrupts` | Ignore interrupt signals on Unix-like systems |

## Examples

```bash
idlebox printf 'hello\n' | idlebox tee output.txt
idlebox printf 'again\n' | idlebox tee -a output.txt
idlebox cat input.bin | idlebox tee copy-one.bin copy-two.bin >/dev/null
```

## Implementation Notes

- Located in `src/applets/tee.rs`
- Uses a fixed 16 KiB streaming buffer
- Continues writing files if the standard-output pipe closes early
- Reports per-file open and write failures while continuing other destinations

## See Also

- [cat](cat.md)
- [printf](printf.md)
