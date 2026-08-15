# 系统架构概览

> **其他语言：** [English](../en/architecture.md)

IdleBox 采用受 BusyBox 启发的模块化、多调用二进制架构。单一二进制文件作为所有 Applet 的入口点，根据调用名称或子命令分发到正确的实现。

## 设计理念

> **告别 Busy，拥抱 Idle。**

IdleBox 以现代 Rust 语言重新诠释了经典的 BusyBox 理念：

- **零依赖** — 仅使用 Rust 标准库，不引入任何第三方 crate
- **灵活模块化** — 通过统一的 Applet 接口扩展功能，同时保持单一多调用二进制
- **体积与性能优先** — 通过 LTO、`opt-level = "z"`、`codegen-units = 1` 和 `strip` 控制 Release 构建开销
- **渐进兼容** — 从常见 Unix/POSIX 工作流开始，逐步扩展 BusyBox 和 GNU 兼容行为
- **高颜值输出** — 内置 ANSI 彩色支持，带来赏心悦目的终端体验

### 当前阶段的工程优先级

IdleBox 的长期方向包括提升对 POSIX、BusyBox 和 GNU 工具行为的兼容能力，但当前阶段不以完整替代它们作为开发前提。工作按以下顺序推进：

1. 尽量保持项目灵活、小巧、轻便、高性能，并守住单二进制和零外部依赖的基础
2. 优先优化 IdleBox 自身的架构、正确性、基础功能、用户体验和跨平台一致性
3. 在基础稳定后，先兼容高频实际用法，再逐步覆盖更完整的标准与长尾行为
4. 新功能、抽象和兼容层应通过二进制体积、启动时间、吞吐量与测试结果衡量成本

这套顺序描述的是当前开发策略，并不永久限定项目的长期演进方向。

## 源码结构

```
src/
├── main.rs              # 入口：argv0 分发与用法说明
├── core/
│   ├── mod.rs           # Core 模块导出
│   ├── applet.rs        # Applet trait 定义
│   ├── dispatcher.rs    # Applet 注册表与分发逻辑
│   └── install.rs       # 跨平台 launcher 安装
└── applets/
    ├── mod.rs           # Applet 模块导出
    ├── echo.rs          # echo Applet
    ├── cat.rs           # cat Applet
    ├── ls.rs            # ls Applet（ANSI 彩色）
    ├── ...               # 其他 POSIX 风格 Applet
    └── relax.rs         # relax Applet（IdleBox 特色）
```

## 核心概念

### `Applet` Trait

每个 Applet 都实现定义在 `src/core/applet.rs` 中的 `Applet` trait：

```rust
pub trait Applet {
    fn name(&self) -> &'static str;
    fn description(&self) -> &'static str;
    fn run(&self, args: &[String]) -> Result<i32, Box<dyn std::error::Error>>;
    fn help(&self) { /* 默认实现 */ }
}
```

该 trait 为分发器提供了统一的接口，使其能够以一致的 API 调用任何 Applet。

### 分发器（Dispatcher）

`src/core/dispatcher.rs` 包含 `Dispatcher` 结构体，负责：

1. 维护所有可用 Applet 的注册表
2. 根据名称将传入命令路由到正确的 Applet
3. 统一处理所有 Applet 的 `--help` / `-h` 标志
4. 为 `list` 子命令提供 `list_applets()` 函数

### 调用模式

IdleBox 支持两种调用模式：

#### 1. 子命令模式

```bash
idlebox echo "Hello, World!"
idlebox ls --color=auto -lah
```

二进制名称为 `idlebox`，第一个参数选择要运行的 Applet。

#### 2. 已安装 Launcher 模式（多调用）

```bash
# Unix-like 系统：符号链接 launcher
idlebox --install ./bin
./bin/echo "Hello from a launcher!"
./bin/ls --color=auto
```

```powershell
# Windows：.exe 硬链接，失败时回退为文件副本
.\idlebox.exe --install .\bin
.\bin\echo.exe "Hello from a launcher!"
```

二进制文件检查 `argv[0]` 中的文件名，并在选择 Applet 前移除末尾的 `.exe`。因此，Unix-like 系统可以保留 BusyBox 风格的符号链接调用，Windows 则可以使用普通的可执行 launcher。

## 分发流程

```
main()
  │
  ├─ 解析 argv[0] 中的文件名，并移除末尾的 ".exe"
  │   ├─ "idlebox" → 使用 argv[1] 作为 Applet 名称
  │   └─ 其他      → 使用 launcher 文件名作为 Applet 名称
  │
  ├─ 特殊情况："list" → 打印所有 Applet 并退出
  ├─ 特殊情况："--install" → 安装所有 Applet launcher 并退出
  │
  └─ Dispatcher::dispatch(name, args)
      │
      ├─ 检查 --help / -h → 打印帮助并退出
      │
      └─ 匹配 Applet 名称 → 实例化并运行
          ├─ "echo"  → EchoApplet
          ├─ "cat"   → CatApplet
          ├─ ...
          └─ "relax" → RelaxApplet
```

## 构建优化

`Cargo.toml` 的 Release 配置针对最小二进制体积进行了调优：

```toml
[profile.release]
opt-level = "z"      # 优化体积
lto = true            # 链接时优化
codegen-units = 1     # 单一代码生成单元，获得更好的优化效果
panic = "abort"       # 移除 panic 展开开销
strip = true          # 剥离调试符号
```

这会生成针对体积优化的二进制文件；实际大小取决于目标平台、Rust 工具链和链接方式，适用性应以对应发布产物的测量结果为准。

## 添加新 Applet

1. 创建 `src/applets/my_applet.rs`
2. 实现 `Applet` trait
3. 在 `src/applets/mod.rs` 中导出
4. 在 `src/core/dispatcher.rs` 的 `dispatch()`、`applet_names()` 和 `list_applets()` 中注册

请参阅各 [Applet 文档](applets/) 获取实现示例。
