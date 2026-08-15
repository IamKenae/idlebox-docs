# realpath — 打印规范化绝对路径

> **其他语言：** [English](../../en/applets/realpath.md)

## 语法

```
realpath [选项]... 文件...
```

## 描述

`realpath` 解析全部符号链接与相对路径部分，然后输出规范化绝对路径。路径的每个组成部分都必须存在。

## 选项

| 选项 | 描述 |
|------|------|
| `-e`, `--canonicalize-existing` | 要求所有组成部分存在（默认行为） |
| `-q`, `--quiet` | 无法解析路径时不输出诊断信息 |
| `-z`, `--zero` | 使用 NUL 结束每条输出记录 |

## 示例

```bash
idlebox realpath ./src/../README.md
idlebox realpath -q missing-file
idlebox realpath -z path-one path-two
```

## 实现说明

- 位于 `src/applets/realpath.rs`
- 使用 `std::fs::canonicalize`，对已有路径的行为与 `readlink -f` 一致
- 某个操作数失败后仍继续处理其余路径

## 参见

- [readlink](readlink.md)
- [pwd](pwd.md)
