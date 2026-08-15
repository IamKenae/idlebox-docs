# tar — 创建、查看与解包归档

> **其他语言：** [English](../../en/applets/tar.md)

## 语法

```
tar (-c|-x|-t) [-zv] [-f 归档] [-C 目录] [文件]...
```

## 描述

`tar` 读写 512 字节 POSIX ustar 记录。它会递归归档普通文件与目录，并在不跟随符号链接的情况下保留链接。使用 `-z` 可以让归档数据经过纯 Rust Gzip 后端。

必须且只能指定一种操作模式。省略 `-f` 时，创建模式将归档写入标准输出，查看/解包模式从标准输入读取；也可以显式使用 `-` 作为归档名。

## 选项

| 选项 | 描述 |
|------|------|
| `-c`, `--create` | 创建新归档 |
| `-x`, `--extract` | 解包归档成员 |
| `-t`, `--list` | 仅打印成员名称，不解包 |
| `-f`, `--file 归档` | 读写指定归档 |
| `-z`, `--gzip` | 将 tar 流压缩或解压为 Gzip |
| `-C`, `--directory 目录` | 将目录用作创建基准或解包目标 |
| `-v`, `--verbose` | 创建或解包时打印成员名称 |

短选项可以组合；`-czvf archive.tar.gz files` 等同于分别使用 `-c -z -v -f`。

## 示例

```bash
idlebox tar -cvf source.tar src README.md
idlebox tar -tf source.tar
idlebox tar -xvf source.tar -C restored
idlebox tar -czf source.tar.gz src
idlebox tar -tzf source.tar.gz
```

## 安全与格式说明

- 使用标头前会验证校验和及八进制数字字段。
- 普通文件内容会先写入临时文件，完整读取条目后才发布。
- 输出到文件的归档会先暂存，创建失败不会替换已有归档。
- Unix 文件与目录权限位会恢复；限制性目录权限在子项解包完成后应用。
- 解包时拒绝绝对路径、Windows 盘符路径、反斜杠路径与 `..` 组件。
- 解包不会穿过或覆盖目标路径中的符号链接。
- 拒绝可能逃出解包根目录的符号链接目标。
- 当前支持 POSIX ustar 普通文件、目录和符号链接；暂不支持 GNU/PAX 扩展、设备节点、硬链接记录、稀疏文件及超出 ustar 前缀/名称限制的名称。
- Unix-like 系统可创建符号链接；其他平台遇到含符号链接的归档时会报告不支持。

## 参见

- [gzip](gzip.md)
- [gunzip](gunzip.md)
- [unzip](unzip.md)
