# sha256sum

计算和校验 SHA256 消息摘要。

## 用法

```bash
idlebox sha256sum [选项]... [文件]...
```

## 选项

* `-c, --check`: 从文件中读取 SHA256 校验和并进行检查
* `-b, --binary`: 以二进制模式读取
* `-t, --text`: 以文本模式读取（默认）
* `--status`: 不输出任何内容，仅通过状态码表示成功与否

## 示例

计算文件的 SHA256 哈希值：
```bash
idlebox sha256sum file.txt
```

检查校验和文件中列出的文件的 SHA256 哈希值：
```bash
idlebox sha256sum -c checksums.sha256
```
