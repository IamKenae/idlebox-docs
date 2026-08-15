# sleep — Pause for a Specified Duration

> **Other languages:** [中文](../../zh/applets/sleep.md)

## Synopsis

```
sleep NUMBER[SUFFIX]...
```

## Description

`sleep` pauses execution for the sum of all supplied intervals. Numbers may be fractional.

## Suffixes

| Suffix | Unit |
|--------|------|
| none or `s` | Seconds |
| `m` | Minutes |
| `h` | Hours |
| `d` | Days |

## Examples

```bash
idlebox sleep 0.5
idlebox sleep 2m
idlebox sleep 1h 30m
```

## Implementation Notes

- Located in `src/applets/sleep.rs`
- Uses `std::thread::sleep` and checked `Duration` addition
- Rejects negative, non-finite, unknown-suffix, and overflowing intervals

## See Also

- [relax](relax.md)
