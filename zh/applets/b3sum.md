# b3sum

> **其他语言：** [English](../../en/applets/b3sum.md)
计算和校验 BLAKE3 消息摘要（纯自研实现，支持大文件极致并行分片计算）。

## 用法

```bash
idlebox b3sum [选项]... [文件]...
```

## 选项

* `-c, --check`: 从文件中读取 BLAKE3 校验和并进行检查
* `-b, --binary`: 以二进制模式读取
* `-t, --text`: 以文本模式读取（默认）
* `--status`: 不输出任何内容，仅通过状态码表示成功与否

## 示例

计算大文件的 BLAKE3 哈希值（自动利用多核极速计算）：
```bash
idlebox b3sum big_file.iso
```

检查校验和文件中列出的文件的 BLAKE3 哈希值：
```bash
idlebox b3sum -c checksums.b3
```
