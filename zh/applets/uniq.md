# uniq — 报告或省略重复行

> **其他语言：** [English](../../en/applets/uniq.md)

## 语法

```
uniq [选项]... [输入 [输出]]
```

## 描述

`uniq` Applet 从输入（或标准输入）中过滤相邻的匹配行；提供输出路径时写入该文件，否则写入标准输出。默认情况下，它将相同的连续行合并为单行输出。注意 `uniq` 只检测相邻的重复行——如果输入未分组，请先使用 `sort` 排序。

## 选项

| 选项 | 描述 |
|------|------|
| `-c`, `--count` | 在每行前显示出现次数 |
| `-d`, `--repeated` | 仅输出重复出现的行（出现超过一次） |
| `-u`, `--unique` | 仅输出唯一的（未重复的）行 |
| `-i`, `--ignore-case` | 比较时忽略大小写 |

## 退出状态

| 退出码 | 含义 |
|--------|------|
| 0 | 成功 |
| 1 | 发生错误 |

## 示例

```bash
# 去除相邻重复行
idlebox uniq file.txt

# 统计出现次数
idlebox uniq -c file.txt
# 输出:
#       2 apple
#       3 banana
#       1 cherry

# 仅显示重复行
idlebox uniq -d file.txt

# 仅显示唯一（未重复）行
idlebox uniq -u file.txt

# 忽略大小写比较
idlebox uniq -i file.txt

# 组合计数与重复过滤
idlebox uniq -c -d file.txt
# 输出:
#       2 apple
#       3 banana

# 从 stdin 管道
cat file.txt | idlebox uniq -c

# 将结果直接流式写入输出文件
idlebox uniq -c input.txt output.txt
```

## 实现说明

- 位于 `src/applets/uniq.rs`
- 仅检测相邻重复行（POSIX 行为）
- 计数输出右对齐，列宽 7 个字符
- 忽略大小写模式只保留当前分组的小写比较键
- 流式处理相邻分组，内存占用与最长的一对输入行相关，而不随文件总大小增长
- 拒绝多余操作数；输入和输出拼写相同时直接报错，避免静默截断输入

## 参见

- [sort](sort.md) — 先排序再用 uniq 去除所有重复
- [wc](wc.md) — 统计行数
- [架构概览](../architecture.md)
