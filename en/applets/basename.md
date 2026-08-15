# basename — Strip Directory and Suffix from File Names

> **Other languages:** [中文](../../zh/applets/basename.md)

## Synopsis

```
basename NAME [SUFFIX]
basename OPTION... NAME...
```

## Description

`basename` removes leading directory components from each name. It can also remove a matching suffix without removing the entire resulting name.

## Options

| Option | Description |
|--------|-------------|
| `-a`, `--multiple` | Process every `NAME` operand |
| `-s`, `--suffix=SUFFIX` | Remove `SUFFIX`; implies `-a` |
| `-z`, `--zero` | End records with NUL instead of newline |

## Examples

```bash
idlebox basename /usr/local/bin/tool
# tool

idlebox basename report.txt .txt
# report

idlebox basename -s .log one.log /tmp/two.log
# one
# two
```

## Implementation Notes

- Located in `src/applets/basename.rs`
- Performs lexical path processing and does not access the file system
- Supports both the traditional `NAME [SUFFIX]` form and GNU-style multiple operands

## See Also

- [dirname](dirname.md)
- [realpath](realpath.md)
