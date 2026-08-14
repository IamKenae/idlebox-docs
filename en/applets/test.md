# test / [ — Evaluate Conditional Expressions

> **Other languages:** [中文](../../zh/applets/test.md)

## Synopsis

```
test EXPR
[ EXPR ]
```

## Description

The `test` applet evaluates conditional expressions and returns an exit status. It supports two forms:
- `test EXPR` — evaluates the expression directly
- `[ EXPR ]` — equivalent to `test EXPR`, but requires a closing `]`

Returns:
- **0** if the expression is true
- **1** if the expression is false
- **2** on syntax error

## Operators

### File Tests

| Operator | Description |
|----------|-------------|
| `-e FILE` | FILE exists |
| `-f FILE` | FILE exists and is a regular file |
| `-d FILE` | FILE exists and is a directory |
| `-s FILE` | FILE exists and has size > 0 |
| `-L FILE` | FILE exists and is a symbolic link |
| `-h FILE` | Same as `-L` |

### String Tests

| Operator | Description |
|----------|-------------|
| `-z STR` | STR has zero length |
| `-n STR` | STR has non-zero length |
| `S1 = S2` | Strings are equal |
| `S1 == S2` | Strings are equal (GNU extension) |
| `S1 != S2` | Strings are not equal |

### Numeric Comparisons

| Operator | Description |
|----------|-------------|
| `N1 -eq N2` | N1 equals N2 |
| `N1 -ne N2` | N1 not equals N2 |
| `N1 -gt N2` | N1 greater than N2 |
| `N1 -ge N2` | N1 greater than or equal to N2 |
| `N1 -lt N2` | N1 less than N2 |
| `N1 -le N2` | N1 less than or equal to N2 |

### Logical Operators

| Operator | Description |
|----------|-------------|
| `! EXPR` | Negation |
| `E1 -a E2` | Both expressions are true (AND) |
| `E1 -o E2` | Either expression is true (OR) |

## Examples

```bash
# File tests
idlebox test -f /etc/passwd        # true if regular file
idlebox [ -d /tmp ]                # true if directory
idlebox [ -e /nonexistent ]        # false, file doesn't exist

# String tests
idlebox test -z ""                 # true, empty string
idlebox [ -n "hello" ]             # true, non-empty string
idlebox [ "abc" = "abc" ]          # true, strings equal
idlebox [ "abc" != "def" ]         # true, strings different

# Numeric comparisons
idlebox [ 5 -gt 3 ]                # true
idlebox [ 10 -eq 10 ]              # true
idlebox [ 1 -lt 2 ]                # true

# Logical operators
idlebox [ 1 -eq 1 -a 2 -eq 2 ]    # true (both conditions)
idlebox [ 1 -eq 2 -o 2 -eq 2 ]    # true (either condition)
idlebox [ ! 1 -eq 2 ]              # true (negation)
```

## Implementation Notes

- Located in `src/applets/test.rs`
- Both `test` and `[` are registered as separate applets sharing the same evaluation logic
- The `[` applet validates the closing `]` bracket
- Expression parsing uses recursive descent with proper operator precedence
- Uses only Rust standard library for file system operations

## See Also

- [expr](expr.md) — evaluate arithmetic and string expressions
- [Architecture Overview](../architecture.md)
