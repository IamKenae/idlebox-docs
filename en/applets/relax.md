# relax — Take a Break and Relax

> **Other languages:** [中文](../../zh/applets/relax.md)

## Synopsis

```
relax [SECONDS]
```

## Description

`relax` is IdleBox's signature applet — a gentle reminder to pause and take a break. It idles for a specified number of seconds, then returns a refreshing message.

This applet embodies the "Idle" in IdleBox: sometimes the most productive thing you can do is nothing at all.

## Arguments

| Argument | Description |
|----------|-------------|
| `SECONDS` | Duration to relax in seconds (default: `5`) |

## Examples

```bash
# Default: relax for 5 seconds
idlebox relax
# Output:
# Relaxing for 5 seconds...
# (5 seconds pass)
# Refreshed! Back to work.

# Relax for 10 seconds
idlebox relax 10
# Output:
# Relaxing for 10 seconds...
# (10 seconds pass)
# Refreshed! Back to work.
```

## Implementation Notes

- Located in `src/applets/relax.rs`
- Uses `std::thread::sleep` for the wait duration
- Defaults to 5 seconds if no argument is provided
- Invalid (non-numeric) arguments fall back to the default 5 seconds
- This applet has no flags or options — just pure idleness

## Philosophy

> **Say goodbye to Busy, embrace Idle.**

In a world obsessed with productivity, `relax` is a small act of rebellion. It reminds us that rest is not the opposite of work — it is the foundation of it.

## See Also

- [Architecture Overview](../architecture.md)
