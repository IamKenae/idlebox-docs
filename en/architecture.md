# Architecture Overview

> **Other languages:** [中文](../zh/architecture.md)

IdleBox follows a modular, multi-call binary architecture inspired by BusyBox. A single binary serves as the entry point for all applets, dispatching to the correct implementation based on invocation name or subcommand.

## Design Philosophy

> **Say goodbye to Busy, embrace Idle.**

IdleBox reimagines the classic BusyBox concept in modern Rust:

- **Minimal Pure-Rust Dependencies** — Third-party code is limited to focused Rust crates; compression uses `flate2` with `miniz_oxide`, never a C zlib backend
- **Flexible and Modular** — A uniform applet interface keeps features extensible within one multi-call binary
- **Size and Performance Conscious** — LTO, `opt-level = "z"`, `codegen-units = 1`, and `strip` keep release overhead controlled
- **Progressive Compatibility** — Starts with common Unix/POSIX workflows and incrementally expands BusyBox and GNU behavior
- **Beautiful Output** — Built-in ANSI color support for a delightful terminal experience

### Current Engineering Priorities

IdleBox's long-term direction includes improving behavioral compatibility with POSIX, BusyBox, and GNU tools, but complete replacement is not a prerequisite for the current stage. Work proceeds in this order:

1. Preserve flexibility, a small footprint, low overhead, and high performance while retaining the single-binary foundation and a minimal pure-Rust dependency set
2. Optimize IdleBox itself first: architecture, correctness, core functionality, user experience, and cross-platform consistency
3. Once the foundation is stable, support high-frequency real-world usage before expanding into complete standards and long-tail behavior
4. Evaluate new features, abstractions, and compatibility layers using binary size, startup time, throughput, and test results

This ordering describes the current development strategy and does not permanently constrain the project's long-term evolution.

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
pub trait Applet: Sync {
    fn name(&self) -> &'static str;
    fn description(&self) -> &'static str;
    fn run(&self, args: &[String]) -> Result<i32, Box<dyn std::error::Error>>;
    fn help(&self) { /* default implementation */ }
}
```

This trait provides a uniform interface for the dispatcher to invoke any applet with a consistent API.

### The Dispatcher

`src/core/dispatcher.rs` contains the `Dispatcher` struct, which:

1. Maintains one static registry used by dispatch, listing, and launcher installation
2. Routes incoming commands to the correct applet by name without rebuilding a registry per invocation
3. Handles `--help` and eligible `-h` flags in one argument scan while respecting `--`
4. Exposes the same registered names to `list`, `--list`, and `--install`

### Invocation Modes

IdleBox supports two invocation modes:

#### 1. Subcommand Mode

```bash
idlebox echo "Hello, World!"
idlebox ls --color=auto -lah
idlebox help ls
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
  ├─ Special cases: "--help", "--version", and "help [APPLET]"
  ├─ Special case: "list" / "--list" → print all applets & exit
  ├─ Special case: "--install" → install all applet launchers & exit
  │
  └─ Dispatcher::dispatch(name, args)
      │
      ├─ Look up the applet in the static registry
      ├─ Check for --help / eligible -h → print help & exit
      │
      └─ Run the registered applet
          ├─ "echo"  → EchoApplet
          ├─ "cat"   → CatApplet
          ├─ ...
          └─ "relax" → RelaxApplet
```

## Build Optimization

The package declares Rust 1.85 as its minimum supported toolchain. The `Cargo.toml` release profile is tuned for minimal binary size:

```toml
[profile.release]
opt-level = "z"      # Optimize for size
lto = true            # Link-Time Optimization
codegen-units = 1     # Single codegen unit for better optimization
panic = "abort"       # Remove panic unwinding overhead
strip = true          # Strip debug symbols
```

This produces a binary optimized for size. Its actual size depends on the target platform, Rust toolchain, and linking strategy, so suitability should be judged from measurements of each release artifact.

Archive applets add `flate2` and `crc32fast`. `flate2` disables default features and explicitly selects `rust_backend`, which routes DEFLATE through `miniz_oxide`; therefore these applets do not link zlib or another C compression library.

GitHub Actions separates validation into four workflows:

- **Quality** checks formatting, all-target Clippy and compilation, and rustdoc with warnings denied.
- **Build & Test** runs the full suite and produces release artifacts on native Linux x86_64, macOS, and Windows x86_64. macOS and Windows also lint their platform-specific code paths.
- **Portability** tests the minimum Rust 1.85 toolchain inside Alpine/musl and cross-lints ARMv7/AArch64 Linux with glibc and musl, Windows i686, and Windows ARM64.
- **Binary Size** produces size-optimized glibc and static musl releases and reports their exact byte counts in the workflow summary. Size remains visible for engineering trade-offs without imposing a fixed feature-blocking ceiling.

Pull requests trigger every workflow regardless of whether they are based directly on `main` or stacked on another branch.

## Adding a New Applet

1. Create `src/applets/my_applet.rs`
2. Implement the `Applet` trait
3. Export it in `src/applets/mod.rs`
4. Add one entry to the static `APPLETS` registry in `src/core/dispatcher.rs`, including whether `-h` is available for help

See the individual [applet docs](applets/) for implementation examples.
