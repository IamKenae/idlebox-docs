# Architecture Overview

> **Other languages:** [中文](../zh/architecture.md)

IdleBox follows a modular, multi-call binary architecture inspired by BusyBox. A single binary serves as the entry point for all applets, dispatching to the correct implementation based on invocation name or subcommand.

## Design Philosophy

> **Say goodbye to Busy, embrace Idle.**

IdleBox reimagines the classic BusyBox concept in modern Rust:

- **Zero Dependencies** — Only the Rust standard library; no third-party crates
- **Minimal Footprint** — ~360KB release binary via LTO, `opt-level = "z"`, `codegen-units = 1`, and `strip`
- **POSIX Compatible** — Drop-in replacement for common Unix utilities
- **Beautiful Output** — Built-in ANSI color support for a delightful terminal experience

## Source Tree

```
src/
├── main.rs              # Entry point: argv0 dispatch & usage
├── core/
│   ├── mod.rs           # Core module exports
│   ├── applet.rs        # Applet trait definition
│   ├── dispatcher.rs    # Applet registry & dispatch logic
│   └── install.rs       # Cross-platform launcher installation
└── applets/
    ├── mod.rs           # Applet module exports
    ├── echo.rs          # echo applet
    ├── cat.rs           # cat applet
    ├── ls.rs            # ls applet (ANSI color)
    ├── ...               # Other POSIX-style applets
    └── relax.rs         # relax applet (IdleBox special)
```

## Core Concepts

### The `Applet` Trait

Every applet implements the `Applet` trait defined in `src/core/applet.rs`:

```rust
pub trait Applet {
    fn name(&self) -> &'static str;
    fn description(&self) -> &'static str;
    fn run(&self, args: &[String]) -> Result<i32, Box<dyn std::error::Error>>;
    fn help(&self) { /* default implementation */ }
}
```

This trait provides a uniform interface for the dispatcher to invoke any applet with a consistent API.

### The Dispatcher

`src/core/dispatcher.rs` contains the `Dispatcher` struct, which:

1. Maintains a registry of all available applets
2. Routes incoming commands to the correct applet by name
3. Handles `--help` / `-h` flags uniformly across all applets
4. Provides the `list_applets()` function for the `list` subcommand

### Invocation Modes

IdleBox supports two invocation modes:

#### 1. Subcommand Mode

```bash
idlebox echo "Hello, World!"
idlebox ls --color=auto -lah
```

The binary name is `idlebox`, and the first argument selects the applet.

#### 2. Installed Launcher Mode (Multi-call)

```bash
# Unix-like systems: symbolic-link launchers
idlebox --install ./bin
./bin/echo "Hello from a launcher!"
./bin/ls --color=auto
```

```powershell
# Windows: .exe hard links, with a file-copy fallback
.\idlebox.exe --install .\bin
.\bin\echo.exe "Hello from a launcher!"
```

The binary inspects the filename in `argv[0]` and removes a trailing `.exe` before selecting the applet. This preserves BusyBox-style invocation through symbolic links on Unix-like systems while allowing ordinary executable launchers on Windows.

## Dispatch Flow

```
main()
  │
  ├─ Parse the filename in argv[0] and strip a trailing ".exe"
  │   ├─ "idlebox" → use argv[1] as applet name
  │   └─ other     → use the launcher filename as applet name
  │
  ├─ Special case: "list" → print all applets & exit
  ├─ Special case: "--install" → install all applet launchers & exit
  │
  └─ Dispatcher::dispatch(name, args)
      │
      ├─ Check for --help / -h → print help & exit
      │
      └─ Match applet name → instantiate & run
          ├─ "echo"  → EchoApplet
          ├─ "cat"   → CatApplet
          ├─ ...
          └─ "relax" → RelaxApplet
```

## Build Optimization

The `Cargo.toml` release profile is tuned for minimal binary size:

```toml
[profile.release]
opt-level = "z"      # Optimize for size
lto = true            # Link-Time Optimization
codegen-units = 1     # Single codegen unit for better optimization
panic = "abort"       # Remove panic unwinding overhead
strip = true          # Strip debug symbols
```

This produces a ~360KB binary suitable for embedded systems, containers, and rescue environments.

## Adding a New Applet

1. Create `src/applets/my_applet.rs`
2. Implement the `Applet` trait
3. Export it in `src/applets/mod.rs`
4. Register it in `src/core/dispatcher.rs` in `dispatch()`, `applet_names()`, and `list_applets()`

See the individual [applet docs](applets/) for implementation examples.
