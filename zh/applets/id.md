# id — 打印真实与有效用户及组 ID

> **其他语言：** [English](../../en/applets/id.md)

## 语法

```
id [选项]... [用户]
```

## 描述

`id` Applet 打印当前用户或指定用户的真实与有效用户 ID 和组 ID。不带选项时，输出 UID、GID 和附属组列表。

## 选项

| 选项 | 描述 |
|------|------|
| `-u`, `--user` | 仅输出有效用户 ID |
| `-g`, `--group` | 仅输出有效组 ID |
| `-G`, `--groups` | 输出所有附属组 ID |
| `-n`, `--name` | 输出名称而非数字 ID（需配合 `-u`、`-g` 或 `-G`） |

## 示例

```bash
# 打印完整身份信息
idlebox id

# 仅输出有效 UID
idlebox id -u

# 输出有效用户名
idlebox id -u -n

# 仅输出有效 GID
idlebox id -g

# 输出所有组 ID
idlebox id -G

# 查询指定用户
idlebox id root
```

## 实现说明

- 位于 `src/applets/id.rs`
- 使用 POSIX `getuid()`、`geteuid()`、`getgid()`、`getegid()`、`getpwuid()`、`getpwnam()`、`getgrgid()`、`getgroups()` 和 `getgrouplist()` FFI 调用
- 无 Applet 专属 crate 依赖 — Rust 标准库 + POSIX libc FFI
- 默认输出格式：`uid=1000(用户名) gid=1000(组名) groups=1000(组名),...`

## 参见

- [whoami](whoami.md) — 打印有效用户名
- [su](su.md) — 切换用户
- [架构概览](../architecture.md)
