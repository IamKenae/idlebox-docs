# gzip — 压缩或解压 Gzip 数据

> **其他语言：** [English](../../en/applets/gzip.md)

## 语法

```
gzip [选项]... [文件]...
```

## 描述

`gzip` 使用纯 Rust `miniz_oxide` 后端生成 RFC 1952 Gzip 数据流。未指定文件或操作数为 `-` 时，从标准输入读取并写入标准输出。

处理文件时，压缩输出为 `文件.gz`；解压会移除 `.gz`，或将 `.tgz` 映射为 `.tar`。文件操作成功后默认删除输入文件，使用 `-k` 可保留。写入标准输出时始终保留输入文件。

## 选项

| 选项 | 描述 |
|------|------|
| `-d`, `--decompress` | 改为解压模式 |
| `-k`, `--keep` | 成功生成输出后保留输入文件 |
| `-f`, `--force` | 覆盖已有输出文件 |
| `-c`, `--to-stdout` | 将结果写到标准输出 |

短选项可以组合，例如 `-dc` 或 `-kf`。

## 示例

```bash
idlebox gzip report.txt
idlebox gzip -k archive.tar
idlebox gzip -dc report.txt.gz > report.txt
idlebox cat payload.bin | idlebox gzip -c > payload.bin.gz
```

## 安全与实现说明

- 压缩与解压采用流式处理，不缓存完整文件。
- 文件输出先写入目标目录中的临时文件，整个数据流成功后才发布。
- 源文件权限会在临时输出发布前完成应用。
- 除非显式指定 `-f`，否则保护已有目标。
- 支持多成员 Gzip 输入，并由解码器验证校验值。
- `flate2` 关闭默认特性并显式启用纯 Rust `rust_backend`，不会链接 zlib C 库。

## 参见

- [gunzip](gunzip.md)
- [zcat](zcat.md)
- [tar](tar.md)
