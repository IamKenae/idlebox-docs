# env — 在修改后的环境中运行命令

> **其他语言：** [English](../../en/applets/env.md)

## 语法

```
env [选项]... [-] [名称=值]... [命令 [参数]...]
```

## 描述

`env` 构造一个环境并在其中运行命令。不提供命令时，打印最终得到的环境。

## 选项

| 选项 | 描述 |
|------|------|
| `-i`, `--ignore-environment`, `-` | 从空环境开始 |
| `-u 名称`, `--unset=名称` | 删除指定变量 |
| `-0`, `--null` | 使用 NUL 结束打印的条目 |

## 示例

```bash
# 只为一次命令增加变量
idlebox env MODE=production idlebox printenv MODE

# 打印只包含一个变量的干净环境
idlebox env -i HOME=/tmp

# 为一次命令删除变量
idlebox env -u DEBUG command
```

## 退出状态

Applet 返回被执行命令的退出状态。找不到命令时返回 `127`，其他执行失败返回 `126`。

## 实现说明

- 位于 `src/applets/env.rs`
- 使用 `std::process::Command`，不会修改 IdleBox 父进程的环境
- 显式构建子进程环境，使 `-i`、`-u` 与临时赋值能稳定组合

## 参见

- [printenv](printenv.md)
- [true](true.md)
- [false](false.md)
