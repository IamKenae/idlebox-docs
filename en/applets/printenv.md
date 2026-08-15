# printenv — Print Environment Variables

> **Other languages:** [中文](../../zh/applets/printenv.md)

## Synopsis

```
printenv [OPTION]... [VARIABLE]...
```

## Description

With no operands, `printenv` prints all environment entries as `NAME=VALUE`. With variable names, it prints only their values in the requested order.

## Options

| Option | Description |
|--------|-------------|
| `-0`, `--null` | End each output record with NUL |

## Examples

```bash
idlebox printenv PATH
idlebox printenv HOME USER
idlebox printenv -0
```

## Exit Status

The exit status is `1` when any requested variable is missing; existing variables are still printed.

## Implementation Notes

- Located in `src/applets/printenv.rs`
- Streams values directly to standard output

## See Also

- [env](env.md)
