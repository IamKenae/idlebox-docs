# expr — Evaluate Expressions

> **Other languages:** [中文](../../zh/applets/expr.md)

## Synopsis

```
expr EXPRESSION
```

## Description

The `expr` applet evaluates expressions and prints the result to standard output. It supports arithmetic, comparison, logical, and string operations.

Returns:
- **0** if the result is non-null and non-zero
- **1** if the result is null or zero
- **2** on syntax error

## Operators

### Arithmetic

| Operator | Description |
|----------|-------------|
| `+` | Addition |
| `-` | Subtraction |
| `*` | Multiplication |
| `/` | Integer division |
| `%` | Modulo (remainder) |

### Comparison

| Operator | Description |
|----------|-------------|
| `=` | Equal |
| `!=` | Not equal |
| `<` | Less than |
| `<=` | Less than or equal |
| `>` | Greater than |
| `>=` | Greater than or equal |

### Logical

| Operator | Description |
|----------|-------------|
| `\|` | OR — returns first non-null, non-zero value |
| `&` | AND — returns first value if both are non-null and non-zero, else 0 |

### String Operations

| Function | Description |
|----------|-------------|
| `length STR` | Returns the length of STR |
| `substr STR POS LEN` | Returns substring of STR starting at POS (1-based) with length LEN |

## Examples

```bash
# Arithmetic
idlebox expr 1 + 2          # => 3
idlebox expr 10 - 3         # => 7
idlebox expr 5 '*' 4        # => 20 (quote * to avoid shell glob)
idlebox expr 10 / 3         # => 3 (integer division)
idlebox expr 10 % 3         # => 1

# Comparison
idlebox expr 5 > 3          # => 1 (true)
idlebox expr 5 = 5          # => 1 (true)
idlebox expr "abc" = "abc"  # => 1 (string comparison)

# Logical
idlebox expr 0 '|' 5        # => 5 (first non-zero)
idlebox expr 3 '&' 5        # => 3 (both non-zero, return first)
idlebox expr 0 '&' 5        # => 0 (one is zero)

# String operations
idlebox expr length hello   # => 5
idlebox expr substr hello 2 3  # => "ell"
```

## Implementation Notes

- Located in `src/applets/expr.rs`
- Uses recursive descent parsing with proper operator precedence
- Comparison operators attempt numeric comparison first, falling back to string comparison
- The `*` operator must be quoted or escaped in shell to avoid glob expansion
- Uses only Rust standard library

## See Also

- [test](test.md) — evaluate conditional expressions
- [Architecture Overview](../architecture.md)
