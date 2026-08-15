# unzip — 查看与解压 ZIP 归档

> **其他语言：** [English](../../en/applets/unzip.md)

## 语法

```
unzip [选项]... 归档
```

## 描述

`unzip` 读取 ZIP 中央目录，用于查看条目或安全解压。支持 Stored 与原始 Deflate 条目；实现使用纯 Rust DEFLATE 后端，并验证每个解压文件声明的大小和 CRC32。

## 选项

| 选项 | 描述 |
|------|------|
| `-l`, `--list` | 仅查看条目，不解压 |
| `-o`, `--overwrite` | 覆盖已有普通文件 |
| `-d 目录`, `--directory 目录` | 解压到指定目录而不是当前目录 |

选项可以位于归档操作数之前或之后。归档名称以 `-` 开头时，请先使用 `--`。

## 示例

```bash
idlebox unzip -l release.zip
idlebox unzip release.zip -d release
idlebox unzip -o release.zip -d release
```

## 安全与格式说明

- 对本地标头与中央目录执行边界检查和交叉校验。
- 暂存的覆盖输出在发布前会验证 CRC32 与未压缩大小；新文件校验失败时会删除不完整输出。
- 在 Unix-like 系统上会恢复 Unix ZIP 写入器记录的权限位；限制性目录权限在子项解包完成后应用。
- 拒绝绝对路径、盘符名称、NUL 与 `..` 组件，防止 Zip Slip。
- 解压不会穿过或替换符号链接，并拒绝特殊文件条目。
- 默认保护已有文件；`-o` 会先解码到同目录临时文件，再执行替换。
- 支持 data descriptor、UTF-8 名称和传统 CP437 名称。
- 加密归档、ZIP64、分卷归档以及 Stored (0)/Deflate (8) 之外的压缩方法会明确报告不支持。

## 参见

- [tar](tar.md)
- [gzip](gzip.md)
