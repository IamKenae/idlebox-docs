# 系统架构概览

> **其他语言：** [English](../en/architecture.md)

IdleBox 采用受 BusyBox 启发的模块化、多调用二进制架构。单一二进制文件作为所有 Applet 的入口点，根据调用名称或子命令分发到正确的实现。

## 设计理念

> **告别 Busy，拥抱 Idle。**

IdleBox 以现代 Rust 语言重新诠释了经典的 BusyBox 理念：

- **零依赖** — 仅使用 Rust 标准库，不引入任何第三方 crate
- **极致精简** — 通过 LTO、`opt-level = "z"`、`codegen-units = 1` 和 `strip` 优化，Release 二进制仅约 360KB
- **POSIX 兼容** — 常见 Unix 工具的原生替代
- **高颜值输出** — 内置 ANSI 彩色支持，带来赏心悦目的终端体验

## 源码结构

```
src/
├── main.rs              # 入口：argv0 分发与用法说明
├── core/
│   ├── mod.rs           # Core 模块导出
│   ├── applet.rs        # Applet trait 定义
│   └── dispatcher.rs    # Applet 注册表与分发逻辑
└── applets/
    ├── mod.rs           # Applet 模块导出
    ├── echo.rs          # echo Applet
    ├── cat.rs           # cat Applet
    ├── ls.rs            # ls Applet（ANSI 彩色）
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

#### 2. 符号链接模式（多调用）

```bash
ln -s idlebox echo
ln -s idlebox ls
./echo "Hello via symlink!"
./ls --color=auto
```

二进制文件检查 `argv[0]` 来确定运行哪个 Applet，实现 BusyBox 风格的符号链接调用。

## 分发流程

```
main()
  │
  ├─ 解析 argv[0]（二进制名称）
  │   ├─ "idlebox" → 使用 argv[1] 作为 Applet 名称
  │   └─ 其他      → 使用 argv[0] 作为 Applet 名称（符号链接模式）
  │
  ├─ 特殊情况："list" → 打印所有 Applet 并退出
  │
  └─ Dispatcher::dispatch(name, args)
      │
      ├─ 检查 --help / -h → 打印帮助并退出
      │
      └─ 匹配 Applet 名称 → 实例化并运行
          ├─ "echo"  → EchoApplet
          ├─ "cat"   → CatApplet
          ├─ "ls"    → LsApplet
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

这会产生一个约 360KB 的二进制文件，适用于嵌入式系统、容器环境和救援场景。

## 添加新 Applet

1. 创建 `src/applets/my_applet.rs`
2. 实现 `Applet` trait
3. 在 `src/applets/mod.rs` 中导出
4. 在 `src/core/dispatcher.rs` 中注册（`dispatch()` 和 `list_applets()` 两处）

请参阅各 [Applet 文档](applets/) 获取实现示例。
