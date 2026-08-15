# IdleBox Documentation / 空闲盒文档

> **[中文文档](README-zh.md)**

Welcome to the official documentation repository for **IdleBox** — an independent, lightweight, and visually polished multi-call toolbox inspired by BusyBox, written in pure Rust with zero external dependencies.

## Repository Structure

```
idlebox-docs/
├── en/                         # English documentation
│   ├── architecture.md         # System architecture & design
│   └── applets/                # Applet reference guides
│       ├── basename.md
│       ├── echo.md
│       ├── cat.md
│       ├── ls.md
│       ├── mkdir.md
│       ├── rm.md
│       ├── cp.md
│       ├── mv.md
│       ├── touch.md
│       ├── head.md
│       ├── tail.md
│       ├── grep.md
│       ├── chmod.md
│       ├── chown.md
│       ├── chgrp.md
│       ├── df.md
│       ├── du.md
│       ├── ps.md
│       ├── kill.md
│       ├── free.md
│       ├── uptime.md
│       ├── ln.md
│       ├── readlink.md
│       ├── uname.md
│       ├── test.md
│       ├── expr.md
│       ├── find.md
│       ├── wc.md
│       ├── sort.md
│       ├── uniq.md
│       ├── cut.md
│       ├── tr.md
│       ├── id.md
│       ├── whoami.md
│       ├── su.md
│       ├── relax.md
│       ├── dirname.md
│       ├── env.md
│       ├── false.md
│       ├── printf.md
│       ├── printenv.md
│       ├── pwd.md
│       ├── realpath.md
│       ├── sleep.md
│       ├── tee.md
│       ├── true.md
│       └── install.md
├── zh/                         # Chinese documentation (中文文档)
│   ├── architecture.md         # 系统架构与设计
│   └── applets/                # Applet 命令参考
│       ├── basename.md
│       ├── echo.md
│       ├── cat.md
│       ├── ls.md
│       ├── mkdir.md
│       ├── rm.md
│       ├── cp.md
│       ├── mv.md
│       ├── touch.md
│       ├── head.md
│       ├── tail.md
│       ├── grep.md
│       ├── chmod.md
│       ├── chown.md
│       ├── chgrp.md
│       ├── df.md
│       ├── du.md
│       ├── ps.md
│       ├── kill.md
│       ├── free.md
│       ├── uptime.md
│       ├── ln.md
│       ├── readlink.md
│       ├── uname.md
│       ├── test.md
│       ├── expr.md
│       ├── find.md
│       ├── wc.md
│       ├── sort.md
│       ├── uniq.md
│       ├── cut.md
│       ├── tr.md
│       ├── id.md
│       ├── whoami.md
│       ├── su.md
│       ├── relax.md
│       ├── dirname.md
│       ├── env.md
│       ├── false.md
│       ├── printf.md
│       ├── printenv.md
│       ├── pwd.md
│       ├── realpath.md
│       ├── sleep.md
│       ├── tee.md
│       ├── true.md
│       └── install.md
└── LICENSE                     # CC BY-SA 4.0
```

## Quick Links

### English

- [Architecture Overview](en/architecture.md)
- [Applet: basename](en/applets/basename.md)
- [Applet: dirname](en/applets/dirname.md)
- [Applet: env](en/applets/env.md)
- [Applet: false](en/applets/false.md)
- [Applet: printf](en/applets/printf.md)
- [Applet: printenv](en/applets/printenv.md)
- [Applet: pwd](en/applets/pwd.md)
- [Applet: realpath](en/applets/realpath.md)
- [Applet: sleep](en/applets/sleep.md)
- [Applet: tee](en/applets/tee.md)
- [Applet: true](en/applets/true.md)
- [Applet: echo](en/applets/echo.md)
- [Applet: cat](en/applets/cat.md)
- [Applet: ls](en/applets/ls.md)
- [Applet: mkdir](en/applets/mkdir.md)
- [Applet: rm](en/applets/rm.md)
- [Applet: cp](en/applets/cp.md)
- [Applet: mv](en/applets/mv.md)
- [Applet: touch](en/applets/touch.md)
- [Applet: head](en/applets/head.md)
- [Applet: tail](en/applets/tail.md)
- [Applet: grep](en/applets/grep.md)
- [Applet: chmod](en/applets/chmod.md)
- [Applet: chown](en/applets/chown.md)
- [Applet: chgrp](en/applets/chgrp.md)
- [Applet: df](en/applets/df.md)
- [Applet: du](en/applets/du.md)
- [Applet: ps](en/applets/ps.md)
- [Applet: kill](en/applets/kill.md)
- [Applet: free](en/applets/free.md)
- [Applet: uptime](en/applets/uptime.md)
- [Applet: ln](en/applets/ln.md)
- [Applet: readlink](en/applets/readlink.md)
- [Applet: uname](en/applets/uname.md)
- [Applet: test](en/applets/test.md)
- [Applet: expr](en/applets/expr.md)
- [Applet: find](en/applets/find.md)
- [Applet: wc](en/applets/wc.md)
- [Applet: sort](en/applets/sort.md)
- [Applet: uniq](en/applets/uniq.md)
- [Applet: cut](en/applets/cut.md)
- [Applet: tr](en/applets/tr.md)
- [Applet: id](en/applets/id.md)
- [Applet: whoami](en/applets/whoami.md)
- [Applet: su](en/applets/su.md)
- [Applet: relax](en/applets/relax.md)
- [--install: Automated Deployment](en/applets/install.md)

### 中文

- [架构概览](zh/architecture.md)
- [Applet: basename](zh/applets/basename.md)
- [Applet: dirname](zh/applets/dirname.md)
- [Applet: env](zh/applets/env.md)
- [Applet: false](zh/applets/false.md)
- [Applet: printf](zh/applets/printf.md)
- [Applet: printenv](zh/applets/printenv.md)
- [Applet: pwd](zh/applets/pwd.md)
- [Applet: realpath](zh/applets/realpath.md)
- [Applet: sleep](zh/applets/sleep.md)
- [Applet: tee](zh/applets/tee.md)
- [Applet: true](zh/applets/true.md)
- [Applet: echo](zh/applets/echo.md)
- [Applet: cat](zh/applets/cat.md)
- [Applet: ls](zh/applets/ls.md)
- [Applet: mkdir](zh/applets/mkdir.md)
- [Applet: rm](zh/applets/rm.md)
- [Applet: cp](zh/applets/cp.md)
- [Applet: mv](zh/applets/mv.md)
- [Applet: touch](zh/applets/touch.md)
- [Applet: head](zh/applets/head.md)
- [Applet: tail](zh/applets/tail.md)
- [Applet: grep](zh/applets/grep.md)
- [Applet: chmod](zh/applets/chmod.md)
- [Applet: chown](zh/applets/chown.md)
- [Applet: chgrp](zh/applets/chgrp.md)
- [Applet: df](zh/applets/df.md)
- [Applet: du](zh/applets/du.md)
- [Applet: ps](zh/applets/ps.md)
- [Applet: kill](zh/applets/kill.md)
- [Applet: free](zh/applets/free.md)
- [Applet: uptime](zh/applets/uptime.md)
- [Applet: ln](zh/applets/ln.md)
- [Applet: readlink](zh/applets/readlink.md)
- [Applet: uname](zh/applets/uname.md)
- [Applet: test](zh/applets/test.md)
- [Applet: expr](zh/applets/expr.md)
- [Applet: find](zh/applets/find.md)
- [Applet: wc](zh/applets/wc.md)
- [Applet: sort](zh/applets/sort.md)
- [Applet: uniq](zh/applets/uniq.md)
- [Applet: cut](zh/applets/cut.md)
- [Applet: tr](zh/applets/tr.md)
- [Applet: id](zh/applets/id.md)
- [Applet: whoami](zh/applets/whoami.md)
- [Applet: su](zh/applets/su.md)
- [Applet: relax](zh/applets/relax.md)
- [--install: 自动化部署](zh/applets/install.md)

## About IdleBox

IdleBox reimagines the classic BusyBox concept in modern Rust. The name embodies our philosophy:

> **Say goodbye to Busy, embrace Idle.**

While BusyBox has powered embedded Linux for over two decades, IdleBox brings the same multi-call binary paradigm into the Rust ecosystem with zero dependencies, compact builds, and beautiful ANSI-colored terminal output.

The current stage prioritizes improving IdleBox's structure, core functionality, and user experience while preserving flexibility, a small footprint, low overhead, and high performance. Compatibility with POSIX, BusyBox, and GNU behavior then expands incrementally, starting with common workflows. This ordering is a current engineering strategy and does not permanently constrain the project's long-term direction.

## Platform Support

| Platform | Status | Notes |
|----------|--------|-------|
| Linux | Full | All 47 applets supported |
| macOS | Full | All 47 applets supported |
| Windows | Partial | See details below |

### Windows Applet Compatibility

| Applet | Windows Support | Notes |
|--------|----------------|-------|
| basename, cat, cp, cut, dirname, echo, env, expr, false, find, grep, head, mkdir, mv, printf, printenv, pwd, readlink, realpath, relax, rm, sleep, sort, tail, tee, test, touch, tr, true, uniq, wc | Full | Cross-platform, identical behavior |
| ls, du, ln | Full | Adapted for Windows (no Unix file types/modes) |
| df, free, ps, uptime, whoami, uname, kill | Partial | Uses Windows APIs (wmic, tasklist, taskkill) |
| chmod, chgrp, chown, id, su | Not supported | Unix-only concepts (permissions, ownership, signals) |

`idlebox --install` is supported on both Unix-like systems and Windows. It creates symbolic links on Unix-like systems and `.exe` hard links on Windows, with a file-copy fallback when hard links are unavailable.

## License

Documentation is licensed under [CC BY-SA 4.0](LICENSE).

Copyright (c) IdleBox Contributors.
