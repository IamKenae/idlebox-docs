# 空闲盒文档 / IdleBox Documentation

> **[English](README.md)**

欢迎来到 **IdleBox（空闲盒）** 的官方文档仓库 —— 一个独立、轻量、高颜值的 BusyBox/POSIX 兼容工具箱，使用纯 Rust 编写，零外部依赖。

## 仓库结构

```
idlebox-docs/
├── en/                         # English documentation
│   ├── architecture.md         # System architecture & design
│   └── applets/                # Applet reference guides
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
│       ├── df.md
│       ├── du.md
│       ├── ps.md
│       ├── kill.md
│       ├── free.md
│       ├── uptime.md
│       ├── relax.md
│       └── install.md
├── zh/                         # 中文文档
│   ├── architecture.md         # 系统架构与设计
│   └── applets/                # Applet 命令参考
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
│       ├── df.md
│       ├── du.md
│       ├── ps.md
│       ├── kill.md
│       ├── free.md
│       ├── uptime.md
│       ├── relax.md
│       └── install.md
└── LICENSE                     # CC BY-SA 4.0
```

## 快速导航

### English

- [Architecture Overview](en/architecture.md)
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
- [Applet: df](en/applets/df.md)
- [Applet: du](en/applets/du.md)
- [Applet: ps](en/applets/ps.md)
- [Applet: kill](en/applets/kill.md)
- [Applet: free](en/applets/free.md)
- [Applet: uptime](en/applets/uptime.md)
- [Applet: relax](en/applets/relax.md)
- [--install: Automated Deployment](en/applets/install.md)

### 中文

- [架构概览](zh/architecture.md)
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
- [Applet: df](zh/applets/df.md)
- [Applet: du](zh/applets/du.md)
- [Applet: ps](zh/applets/ps.md)
- [Applet: kill](zh/applets/kill.md)
- [Applet: free](zh/applets/free.md)
- [Applet: uptime](zh/applets/uptime.md)
- [Applet: relax](zh/applets/relax.md)
- [--install: 自动化部署](zh/applets/install.md)

## 关于空闲盒

IdleBox 以现代 Rust 语言重新诠释了经典的 BusyBox 理念。项目名蕴含了我们的设计哲学：

> **告别 Busy，拥抱 Idle。**

BusyBox 在嵌入式 Linux 领域服务了二十余年，而 IdleBox 将这种"多调用二进制"的范式带入 Rust 生态 —— 零依赖、约 360KB 的极致体积、以及赏心悦目的 ANSI 彩色终端输出。

## 许可证

文档基于 [CC BY-SA 4.0](LICENSE) 协议授权。

版权所有 (c) IdleBox Contributors.
