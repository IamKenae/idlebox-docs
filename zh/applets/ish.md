# ish — Idle Shell 解释器

> **其他语言：** [English](../../en/applets/ish.md)

## 语法

```
ish [选项] [脚本]
ish -c 命令
sh [选项] [脚本]
ash [选项] [脚本]
```

## 描述

`ish`（Idle Shell）Applet 是一个完全使用 Rust 构建的 POSIX 兼容 Shell 解释器，零外部依赖。它提供完整的 Shell 环境，支持：

- 交互式 REPL 模式
- 脚本文件执行
- 使用 `-c` 执行命令行
- 环境变量展开（`$VAR`、`${VAR}`）
- 管道（`|`）
- 逻辑运算符（`&&`、`||`）
- 命令分隔符（`;`）
- 后台执行（`&`）
- 重定向（`>`、`>>`、`<`、`2>`）
- 流程控制（`if/then/elif/else/fi`、`for/in/do/done`、`while/do/done`）
- Shell 内置命令（`cd`、`exit`、`export`、`unset`、`alias`、`unalias`、`read`、`pwd`）
- 内存级 Applet 派发（直接函数调用 IdleBox Applet，无需 fork/exec）

`sh` 和 `ash` 命令是指向 `ish` 的符号链接，提供完全相同的功能。

## 选项

| 选项     | 描述                   |
|----------|------------------------|
| `-c 命令`| 执行命令并退出         |
| `脚本`   | 执行脚本文件           |
| （无）   | 启动交互式 Shell       |

## Shell 内置命令

| 命令      | 描述                         |
|-----------|------------------------------|
| `cd`      | 切换目录                     |
| `exit`    | 退出 Shell，可指定状态码     |
| `export`  | 设置环境变量                 |
| `unset`   | 取消设置环境变量或别名       |
| `alias`   | 定义或显示别名               |
| `unalias` | 删除别名定义                 |
| `read`    | 从标准输入读取一行           |
| `pwd`     | 打印工作目录                 |

## 示例

### 交互模式

```bash
# 启动交互式 Shell
idlebox ish
ish$ echo "Hello, World!"
Hello, World!
ish$ export GREETING=Hi
ish$ echo $GREETING
Hi
ish$ exit
```

### 命令模式

```bash
# 执行单个命令
idlebox ish -c "echo hello"
# 输出: hello

# 执行管道
idlebox ish -c "ls -l | grep txt | wc -l"
# 输出: .txt 文件的数量

# 使用逻辑运算符执行
idlebox ish -c "true && echo success || echo failure"
# 输出: success
```

### 脚本模式

```bash
# 创建脚本文件
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

# 执行脚本
idlebox ish script.sh
# 输出:
# Hello, World!
# Count: 1
# Count: 2
# Count: 3
# Condition met
```

### 重定向

```bash
# 输出重定向
idlebox ish -c "echo hello > file.txt"

# 追加重定向
idlebox ish -c "echo world >> file.txt"

# 输入重定向
idlebox ish -c "cat < file.txt"

# 错误重定向
idlebox ish -c "cmd 2> error.log"
```

### 使用 sh 和 ash 别名

```bash
# 三个命令等价
idlebox ish -c "echo hello"
idlebox sh -c "echo hello"
idlebox ash -c "echo hello"
```

## 实现说明

- 位于 `src/applets/sh/`
- 纯 Rust 实现，零外部依赖
- 词法分析器：`lexer.rs` - 对 Shell 输入进行分词
- 语法解析器：`parser.rs` - 从标记构建 AST
- 执行器：`evaluator.rs` - 执行 AST 节点
- 内置命令：`builtins.rs` - Shell 内置命令
- 主 Applet：`ish.rs` - REPL、脚本和命令模式
- IdleBox Applet 的内存级派发（无 fork/exec 开销）
- 使用操作系统级管道正确处理管道
- 环境变量向子进程传播
- POSIX 兼容的语法和语义

## 性能

`ish` Shell 通过内存级派发为 IdleBox Applet 实现了显著的性能提升：

- **传统 Shell**：每个命令都需要 fork() + exec()
- **ish 与 IdleBox Applet**：直接函数调用（无进程创建）
- **外部命令**：通过 `std::process::Command` 标准 fork() + exec()

这使得 IdleBox Applet 的管道比传统 Shell 快得多。

## 参见

- [echo](echo.md) — 输出文本到标准输出
- [cat](cat.md) — 连接并打印文件
- [grep](grep.md) — 搜索文本模式
- [架构概览](../architecture.md)
