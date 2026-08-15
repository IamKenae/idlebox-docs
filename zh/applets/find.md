# find — 搜索文件

> **其他语言：** [English](../../en/applets/find.md)

## 语法

```
find [路径...] [选项]
```

## 描述

`find` Applet 递归搜索目录树中匹配指定条件的文件。不指定路径时，默认为当前目录（`.`）。支持并行多线程遍历，在大型目录树上显著提升性能。

## 选项

| 选项 | 描述 |
|------|------|
| `-name 模式` | 使用 glob 模式匹配文件名（例如 `*.rs`、`test_??.txt`） |
| `-type 类型` | 按类型过滤：`f`（普通文件）、`d`（目录）、`l`（符号链接） |
| `-maxdepth N` | 限制递归深度（0 = 仅起始路径） |
| `-empty` | 仅匹配空文件或空目录 |
| `-j`, `--threads N` | 使用 N 个线程进行并行目录遍历（默认：自动检测 CPU 核心数） |

## 并行目录遍历器

`-j` / `--threads` 选项启用基于 Rust 标准库线程的并行目录遍历。搜索深层或大型目录树时，工作负载会分配到多个工作线程，显著减少 I/O 等待时间。

**核心特性：**
- 未指定 `-j` 时自动检测 CPU 核心数
- 共享队列的动态工作窃取实现最优负载均衡
- 排序输出保证跨运行的确定性结果
- 指定 `-j 1` 时回退到单线程模式
- 可通过 `-j N` 显式设置线程数（例如 `-j 8` 表示 8 个线程）

**性能优势：**
- 深层目录树从并行 I/O 操作中获益
- 多层级文件树随可用 CPU 核心数线性扩展
- 零外部依赖 - 纯 Rust 标准库实现

## Glob 模式语法

`-name` 选项支持简单的 glob 模式：
- `*` 匹配任意字符序列
- `?` 匹配单个字符
- 其他所有字符字面匹配

## 示例

```bash
# 查找所有 Rust 源文件
idlebox find . -name "*.rs"

# 查找所有目录
idlebox find /tmp -type d

# 限制深度查找文件
idlebox find . -name "*.txt" -maxdepth 2

# 查找空文件和空目录
idlebox find . -empty

# 组合选项
idlebox find . -type f -name "*.log" -empty

# 查找符号链接
idlebox find /usr -type l

# 使用 4 个线程进行并行搜索
idlebox find . -name "*.rs" -j 4

# 自动检测线程数的并行搜索
idlebox find /var -type f -j 8
```

## 实现说明

- 位于 `src/applets/find.rs`
- 使用 `std::fs::read_dir` 进行目录遍历
- Glob 匹配使用简单状态机实现（无外部正则表达式库）
- 结果在每个目录层级内按字母顺序排序
- 使用 `symlink_metadata` 正确识别符号链接而不跟随它们
- 仅使用 Rust 标准库
- 并行引擎使用工作窃取队列和原子活跃线程追踪
- 通过 `std::sync::Mutex` 和 `std::sync::Arc` 实现线程同步

## 参见

- [ls](ls.md) — 列出目录内容
- [test](test.md) — 文件测试操作符
- [架构概览](../architecture.md)
