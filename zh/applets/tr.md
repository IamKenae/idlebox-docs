# tr — 转换或删除字符

> **其他语言：** [English](../../en/applets/tr.md)

## 语法

```
tr [选项]... SET1 [SET2]
```

## 描述

`tr` Applet 从标准输入读取并写入标准输出。可以将 SET1 中的字符转换为 SET2 中的字符、删除匹配 SET1 的字符、或压缩重复字符。

字符集支持范围扩展：`a-z` 扩展为所有小写字母，`0-9` 扩展为所有数字等。

## 选项

| 选项 | 描述 |
|------|------|
| `-d`, `--delete` | 删除 SET1 中的字符 |
| `-s`, `--squeeze-repeats` | 将连续重复字符压缩为单个字符 |

## 退出状态

| 退出码 | 含义 |
|--------|------|
| 0 | 成功 |
| 1 | 发生错误 |

## 示例

```bash
# 小写转大写
echo "hello" | idlebox tr a-z A-Z
# 输出: HELLO

# 删除数字
echo "abc123def" | idlebox tr -d 0-9
# 输出: abcdef

# 删除回车符
echo -e "hello\r\nworld" | idlebox tr -d '\r'

# 压缩重复空格
echo "hello    world" | idlebox tr -s ' '
# 输出: hello world

# 转换并压缩
echo "aabbcc" | idlebox tr -s a-c x
# 输出: xxx

# 类 ROT13 变换
echo "hello" | idlebox tr a-z n-za-m
# 输出: uryyb
```

## 实现说明

- 位于 `src/applets/tr.rs`
- 始终从 stdin 读取（不接受文件参数）
- 字符范围如 `a-z` 会扩展为单个字符
- 当 SET2 比 SET1 短时，SET2 的最后一个字符会重复
- 压缩模式将连续的匹配字符压缩为一个
- 删除模式移除 SET1 中的所有字符

## 参见

- [cat](cat.md) — 读取文件内容
- [grep](grep.md) — 模式匹配
- [架构概览](../architecture.md)
