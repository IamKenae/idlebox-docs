# --install — 自动化部署 Applet

> **其他语言：** [English](../../en/applets/install.md)

## 语法

```
idlebox --install [路径]
```

## 描述

`--install` 命令通过在目标目录中创建适合当前平台的 launcher，部署所有已注册的 IdleBox Applet。每个 launcher 都以对应 Applet 的名称复用当前 `idlebox` 二进制文件。IdleBox 从 `argv[0]` 读取该名称，并分发到相应的 Applet。

这是将 IdleBox Applet 安装到系统全局或自定义 `PATH` 目录的推荐方式。

| 平台 | Launcher | 默认目标目录 |
|------|----------|--------------|
| Unix-like 系统 | 符号链接 | `/usr/local/bin` |
| Windows | `<applet>.exe` 硬链接；失败时回退为文件副本 | `%LOCALAPPDATA%\IdleBox\bin`；若不可用则回退到 `%USERPROFILE%\.local\bin` |

## 参数

| 参数 | 描述 |
|------|------|
| `[路径]` | 可选的目标目录；指定后会覆盖当前平台的默认目录。 |

## 行为

- 若目标目录不存在，自动创建。
- 从 Dispatcher 获取完整的 Applet 列表，并为每个已注册名称创建一个 launcher。
- 在 Unix-like 系统上创建符号链接。若 launcher 与 `idlebox` 位于同一目录，则使用相对目标；否则使用二进制文件的规范路径。
- 在 Windows 上创建 `<applet>.exe` 硬链接。如果无法创建硬链接（例如跨文件系统），则回退为独占创建的文件副本。
- 先在目标旁的临时路径创建 launcher，再移动到最终位置。已有文件或 launcher 会被直接替换；若同名目标是目录，则报错并保留该目录。
- 为每个 launcher 输出实际安装方式：`symbolic link`、`hard link` 或 `copy`。
- 支持 Unix-like 系统和 Windows；其他平台会返回“不支持的平台”错误。

## 示例

```bash
# Unix：安装到默认位置
idlebox --install
# 输出:
# Installing IdleBox applets to /usr/local/bin...
#   Installed: /usr/local/bin/cat (symbolic link)
#   Installed: /usr/local/bin/echo (symbolic link)
#   ...
# Done. 36 applets installed.

# 安装到自定义目录
idlebox --install ./bin

# 直接使用已安装的 Applet
./bin/echo "hello from a launcher"
./bin/ls -lah
```

Windows PowerShell 示例：

```powershell
# 安装到 %LOCALAPPDATA%\IdleBox\bin
.\idlebox.exe --install
# 输出:
# Installing IdleBox applets to C:\Users\me\AppData\Local\IdleBox\bin...
#   Installed: C:\Users\me\AppData\Local\IdleBox\bin\cat.exe (hard link)
#   ...
# Done. 36 applets installed.

# 安装到自定义目录并直接调用
.\idlebox.exe --install .\bin
.\bin\echo.exe "hello from a launcher"
```

## 注意事项

- Windows 硬链接 launcher 与当前 `idlebox.exe` 共享同一份文件数据，而复制回退得到的是独立快照。替换原始二进制文件后，应重新运行 `--install`，确保所有 launcher 均已刷新。
- 重复运行 `--install` 会刷新已有 launcher；它绝不会删除与 launcher 同名的目录。
- 安装完成后，请确保目标目录已加入 `PATH` 环境变量，以便直接通过名称调用 Applet。
- 如需卸载，只需删除目标目录中的 launcher 即可。

## 参见

- [架构概览](../architecture.md)
- [echo](echo.md) · [cat](cat.md) · [ls](ls.md) · [relax](relax.md)
