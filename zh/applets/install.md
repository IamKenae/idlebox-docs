# --install — 自动化部署 Applet

> **其他语言：** [English](../../en/applets/install.md)

## 语法

```
idlebox --install [路径]
```

## 描述

`--install` 命令通过在一目标目录下创建符号链接（symlink）来自动部署所有已注册的 IdleBox Applet。每个符号链接都指向当前的 `idlebox` 二进制文件，从而实现多调用二进制模式 —— 通过不同的符号链接名调用时，会自动分发到对应的 Applet。

这是将 IdleBox Applet 安装到系统全局或自定义 `PATH` 目录的推荐方式。

## 参数

| 参数 | 描述 |
|------|------|
| `[路径]` | 符号链接的目标目录。省略时默认为 `/usr/local/bin`。 |

## 行为

- 若目标目录不存在，自动创建。
- 遍历所有已注册的 Applet（`cat`、`echo`、`ls`、`relax`）。
- 为每个 Applet 创建指向当前 `idlebox` 二进制的符号链接。
- 若目标位置已存在文件或符号链接，无需确认直接覆盖。
- 使用 `std::os::unix::fs::symlink` 实现 —— 仅支持 Unix-like 系统（Linux、macOS、BSD）。在其他平台上会输出错误提示。

## 示例

```bash
# 安装到默认位置（/usr/local/bin）
idlebox --install
# 输出:
# Installing IdleBox applets to /usr/local/bin...
#   Created symlink: /usr/local/bin/cat -> idlebox
#   Created symlink: /usr/local/bin/echo -> idlebox
#   Created symlink: /usr/local/bin/ls -> idlebox
#   Created symlink: /usr/local/bin/relax -> idlebox
# Done. 4 applets installed.

# 安装到自定义目录
idlebox --install /tmp/mybin
# 输出:
# Installing IdleBox applets to /tmp/mybin...
#   Created symlink: /tmp/mybin/cat -> idlebox
#   ...

# 直接使用已安装的 Applet
echo "hello" | /tmp/mybin/cat
/tmp/mybin/ls -lah /tmp
```

## 注意事项

- 当目标目录与 `idlebox` 二进制所在目录不同时，符号链接使用绝对路径；当安装到二进制所在目录时，使用相对路径。
- 安装完成后，请确保目标目录已加入 `$PATH`，以便直接通过名称调用 Applet。
- 如需卸载，只需删除目标目录中的符号链接即可。

## 参见

- [架构概览](../architecture.md)
- [echo](echo.md) · [cat](cat.md) · [ls](ls.md) · [relax](relax.md)
