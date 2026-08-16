# ish — Idle Shell Interpreter

> **Other languages:** [中文](../../zh/applets/ish.md)

## Synopsis

```
ish [OPTIONS] [SCRIPT]
ish -c COMMAND
sh [OPTIONS] [SCRIPT]
ash [OPTIONS] [SCRIPT]
```

## Description

The `ish` (Idle Shell) applet is a POSIX-compatible shell interpreter built entirely in Rust with zero external dependencies. It provides a complete shell environment with support for:

- Interactive REPL mode
- Script file execution
- Command-line execution with `-c`
- Environment variable expansion (`$VAR`, `${VAR}`)
- Pipes (`|`)
- Logical operators (`&&`, `||`)
- Command separators (`;`)
- Background execution (`&`)
- Redirections (`>`, `>>`, `<`, `2>`)
- Control flow (`if/then/elif/else/fi`, `for/in/do/done`, `while/do/done`)
- Shell built-in commands (`cd`, `exit`, `export`, `unset`, `alias`, `unalias`, `read`, `pwd`)
- In-memory applet dispatching (direct function calls to IdleBox applets without fork/exec)

The `sh` and `ash` commands are symbolic links to `ish` and provide identical functionality.

## Options

| Option   | Description                       |
|----------|-----------------------------------|
| `-c CMD` | Execute CMD and exit              |
| `SCRIPT` | Execute script file               |
| (none)   | Start interactive shell           |

## Shell Built-in Commands

| Command   | Description                                      |
|-----------|--------------------------------------------------|
| `cd`      | Change directory                                 |
| `exit`    | Exit the shell with optional status code         |
| `export`  | Set environment variables                        |
| `unset`   | Unset environment variables or aliases           |
| `alias`   | Define or display aliases                        |
| `unalias` | Remove alias definitions                         |
| `read`    | Read a line from standard input                  |
| `pwd`     | Print working directory                          |

## Examples

### Interactive Mode

```bash
# Start interactive shell
idlebox ish
ish$ echo "Hello, World!"
Hello, World!
ish$ export GREETING=Hi
ish$ echo $GREETING
Hi
ish$ exit
```

### Command Mode

```bash
# Execute a single command
idlebox ish -c "echo hello"
# Output: hello

# Execute a pipeline
idlebox ish -c "ls -l | grep txt | wc -l"
# Output: number of .txt files

# Execute with logical operators
idlebox ish -c "true && echo success || echo failure"
# Output: success
```

### Script Mode

```bash
# Create a script file
cat > script.sh << 'EOF'
#!/usr/bin/env ish
export NAME=World
echo "Hello, $NAME!"

for i in 1 2 3; do
    echo "Count: $i"
done

if true; then
    echo "Condition met"
fi
EOF

# Execute the script
idlebox ish script.sh
# Output:
# Hello, World!
# Count: 1
# Count: 2
# Count: 3
# Condition met
```

### Redirections

```bash
# Output redirection
idlebox ish -c "echo hello > file.txt"

# Append redirection
idlebox ish -c "echo world >> file.txt"

# Input redirection
idlebox ish -c "cat < file.txt"

# Error redirection
idlebox ish -c "cmd 2> error.log"
```

### Using sh and ash Aliases

```bash
# All three commands are equivalent
idlebox ish -c "echo hello"
idlebox sh -c "echo hello"
idlebox ash -c "echo hello"
```

## Implementation Notes

- Located in `src/applets/sh/`
- Pure Rust implementation with zero external dependencies
- Lexer: `lexer.rs` - Tokenizes shell input
- Parser: `parser.rs` - Builds AST from tokens
- Evaluator: `evaluator.rs` - Executes AST nodes
- Builtins: `builtins.rs` - Shell built-in commands
- Main applet: `ish.rs` - REPL, script, and command modes
- In-memory applet dispatching for IdleBox applets (no fork/exec overhead)
- Proper pipeline handling with OS-level pipes
- Environment variable propagation to child processes
- POSIX-compatible syntax and semantics

## Performance

The `ish` shell achieves significant performance improvements for IdleBox applets through in-memory dispatching:

- **Traditional shell**: fork() + exec() for each command
- **ish with IdleBox applets**: Direct function call (no process creation)
- **External commands**: Standard fork() + exec() via `std::process::Command`

This makes pipelines of IdleBox applets extremely fast compared to traditional shells.

## See Also

- [echo](echo.md) — Print text to standard output
- [cat](cat.md) — Concatenate and print files
- [grep](grep.md) — Search text patterns
- [Architecture Overview](../architecture.md)
