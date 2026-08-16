# 空闲盒文档 / IdleBox Documentation

> **[English](README.md)**

欢迎来到 **IdleBox（空闲盒）** 的官方文档仓库 —— 一个受 BusyBox 启发的独立、轻量、高颜值多调用工具箱，采用 Rust 编写，仅保留少量纯 Rust 依赖，不捆绑 C 库。

## 仓库结构

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
│       ├── tar.md
│       ├── gzip.md
│       ├── gunzip.md
│       ├── zcat.md
│       ├── unzip.md
│       ├── true.md
│       └── install.md
├── zh/                         # 中文文档
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
│       ├── tar.md
│       ├── gzip.md
│       ├── gunzip.md
│       ├── zcat.md
│       ├── unzip.md
│       ├── true.md
│       └── install.md
└── LICENSE                     # CC BY-SA 4.0
```

## 快速导航

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
- [Applet: tar](en/applets/tar.md)
- [Applet: gzip](en/applets/gzip.md)
- [Applet: gunzip](en/applets/gunzip.md)
- [Applet: zcat](en/applets/zcat.md)
- [Applet: unzip](en/applets/unzip.md)
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
- [Applet: tar](zh/applets/tar.md)
- [Applet: gzip](zh/applets/gzip.md)
- [Applet: gunzip](zh/applets/gunzip.md)
- [Applet: zcat](zh/applets/zcat.md)
- [Applet: md5sum](zh/applets/md5sum.md)
- [Applet: sha1sum](zh/applets/sha1sum.md)
- [Applet: sha256sum](zh/applets/sha256sum.md)
- [Applet: sha512sum](zh/applets/sha512sum.md)
- [Applet: b3sum](zh/applets/b3sum.md)
- [Applet: unzip](zh/applets/unzip.md)
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

## 关于空闲盒

IdleBox 以现代 Rust 语言重新诠释了经典的 BusyBox 理念。项目名蕴含了我们的设计哲学：

> **告别 Busy，拥抱 Idle。**

BusyBox 在嵌入式 Linux 领域服务了二十余年，而 IdleBox 将这种“多调用二进制”的范式带入 Rust 生态，采用少量纯 Rust 依赖，并继续追求紧凑构建和赏心悦目的终端体验。

当前阶段优先在尽量保持灵活、小巧、轻便与高性能的前提下，优化 IdleBox 自身的结构、基础功能和用户体验；随后再从高频用法开始，逐步提升对 POSIX、BusyBox 和 GNU 工具行为的兼容能力。该顺序是当前工程策略，不永久限定项目的长期方向。

## 平台支持

| 平台 | 状态 | 说明 |
|------|------|------|
| Linux | 完整支持 | 全部 52 个 Applet |
| macOS | 完整支持 | 全部 52 个 Applet |
| Windows | 部分支持 | 详见下方 |

### Windows 平台 Applet 兼容性

| Applet | Windows 支持 | 说明 |
|--------|-------------|------|
| basename, cat, cp, cut, dirname, echo, env, expr, false, find, grep, gunzip, gzip, head, mkdir, mv, printf, printenv, pwd, readlink, realpath, relax, rm, sleep, sort, tail, tee, test, touch, tr, true, uniq, wc, zcat | 完整 | 跨平台，行为一致 |
| ls, du, ln, unzip | 完整 | 已适配 Windows（无 Unix 文件类型/模式；忽略 ZIP 权限位） |
| tar | 部分 | 支持普通文件与目录；不支持解包符号链接 |
| df, free, ps, uptime, whoami, uname, kill | 部分 | 使用 Windows API（wmic, tasklist, taskkill） |
| chmod, chgrp, chown, id, su | 不支持 | Unix 专属概念（权限、属主、信号） |

`idlebox --install` 同时支持 Unix-like 系统和 Windows：Unix-like 系统创建符号链接；Windows 创建 `.exe` 硬链接，无法使用硬链接时回退为文件副本。

## 许可证

文档基于 [CC BY-SA 4.0](LICENSE) 协议授权。

版权所有 (c) IdleBox Contributors.
