# dirname — Strip the Last Component from File Names

> **Other languages:** [中文](../../zh/applets/dirname.md)

## Synopsis

```
dirname [OPTION] NAME...
```

## Description

`dirname` prints each name with its final path component removed. Names without a directory component produce `.`.

## Options

| Option | Description |
|--------|-------------|
| `-z`, `--zero` | End records with NUL instead of newline |

## Examples

```bash
idlebox dirname /usr/local/bin/tool
# /usr/local/bin

idlebox dirname file.txt
# .
```

## Implementation Notes

- Located in `src/applets/dirname.rs`
- Processes paths lexically without requiring them to exist
- Accepts multiple names in one invocation

## See Also

- [basename](basename.md)
- [pwd](pwd.md)
