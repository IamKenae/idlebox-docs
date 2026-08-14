# test / [ — 评估条件表达式

> **其他语言：** [English](../../en/applets/test.md)

## 语法

```
test EXPR
[ EXPR ]
```

## 描述

`test` Applet 评估条件表达式并返回退出状态。它支持两种形式：
- `test EXPR` — 直接评估表达式
- `[ EXPR ]` — 等价于 `test EXPR`，但需要末尾的 `]`

返回值：
- **0** — 表达式为真
- **1** — 表达式为假
- **2** — 语法错误

## 运算符

### 文件测试

| 运算符 | 描述 |
|--------|------|
| `-e FILE` | FILE 存在 |
| `-f FILE` | FILE 存在且为普通文件 |
| `-d FILE` | FILE 存在且为目录 |
| `-s FILE` | FILE 存在且大小大于 0 |
| `-L FILE` | FILE 存在且为符号链接 |
| `-h FILE` | 同 `-L` |

### 字符串测试

| 运算符 | 描述 |
|--------|------|
| `-z STR` | STR 长度为零 |
| `-n STR` | STR 长度非零 |
| `S1 = S2` | 字符串相等 |
| `S1 == S2` | 字符串相等（GNU 扩展） |
| `S1 != S2` | 字符串不相等 |

### 数值比较

| 运算符 | 描述 |
|--------|------|
| `N1 -eq N2` | N1 等于 N2 |
| `N1 -ne N2` | N1 不等于 N2 |
| `N1 -gt N2` | N1 大于 N2 |
| `N1 -ge N2` | N1 大于等于 N2 |
| `N1 -lt N2` | N1 小于 N2 |
| `N1 -le N2` | N1 小于等于 N2 |

### 逻辑运算符

| 运算符 | 描述 |
|--------|------|
| `! EXPR` | 取反 |
| `E1 -a E2` | 两个表达式都为真（与） |
| `E1 -o E2` | 任一表达式为真（或） |

## 示例

```bash
# 文件测试
idlebox test -f /etc/passwd        # 如果是普通文件则为真
idlebox [ -d /tmp ]                # 如果是目录则为真
idlebox [ -e /nonexistent ]        # 假，文件不存在

# 字符串测试
idlebox test -z ""                 # 真，空字符串
idlebox [ -n "hello" ]             # 真，非空字符串
idlebox [ "abc" = "abc" ]          # 真，字符串相等
idlebox [ "abc" != "def" ]         # 真，字符串不同

# 数值比较
idlebox [ 5 -gt 3 ]                # 真
idlebox [ 10 -eq 10 ]              # 真
idlebox [ 1 -lt 2 ]                # 真

# 逻辑运算符
idlebox [ 1 -eq 1 -a 2 -eq 2 ]    # 真（两个条件都满足）
idlebox [ 1 -eq 2 -o 2 -eq 2 ]    # 真（任一条件满足）
idlebox [ ! 1 -eq 2 ]              # 真（取反）
```

## 实现说明

- 位于 `src/applets/test.rs`
- `test` 和 `[` 作为独立的 Applet 注册，共享相同的评估逻辑
- `[` Applet 会验证末尾的 `]` 括号
- 表达式解析使用递归下降法，具有正确的运算符优先级
- 仅使用 Rust 标准库进行文件系统操作

## 参见

- [expr](expr.md) — 评估算术和字符串表达式
- [架构概览](../architecture.md)
