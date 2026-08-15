# env — Run a Command in a Modified Environment

> **Other languages:** [中文](../../zh/applets/env.md)

## Synopsis

```
env [OPTION]... [-] [NAME=VALUE]... [COMMAND [ARG]...]
```

## Description

`env` builds an environment, then runs a command with it. With no command, it prints the resulting environment.

## Options

| Option | Description |
|--------|-------------|
| `-i`, `--ignore-environment`, `-` | Start with an empty environment |
| `-u NAME`, `--unset=NAME` | Remove `NAME` |
| `-0`, `--null` | End printed entries with NUL |

## Examples

```bash
# Add a variable for one command
idlebox env MODE=production idlebox printenv MODE

# Print a clean environment containing one variable
idlebox env -i HOME=/tmp

# Remove a variable for one command
idlebox env -u DEBUG command
```

## Exit Status

The applet returns the command's exit status. A command that cannot be found returns `127`; another execution failure returns `126`.

## Implementation Notes

- Located in `src/applets/env.rs`
- Uses `std::process::Command` and does not modify IdleBox's parent environment
- Builds the child environment explicitly so `-i`, `-u`, and assignments compose predictably

## See Also

- [printenv](printenv.md)
- [true](true.md)
- [false](false.md)
