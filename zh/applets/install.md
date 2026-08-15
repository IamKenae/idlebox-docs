# --install — 自动化部署 Applet

> **其他语言：** [English](../../en/applets/install.md)

## 语法

```
idlebox --install [选项] [路径]
```

## 描述

`--install` 命令通过在目标目录中创建适合当前平台的 launcher，部署所有已注册的 IdleBox Applet。每个 launcher 都以对应 Applet 的名称复用当前 `idlebox` 二进制文件。IdleBox 从 `argv[0]` 读取该名称，并分发到相应的 Applet。

这是将 IdleBox Applet 安装到系统全局或自定义 `PATH` 目录的推荐方式。

| 平台 | Launcher | 默认目标目录 |
|------|----------|--------------|
| Unix-like 系统 | 符号链接 | `/usr/local/bin` |
| Windows | `<applet>.exe` 硬链接；失败时回退为文件副本 | `%LOCALAPPDATA%\IdleBox\bin`；若不可用则回退到 `%USERPROFILE%\.local\bin` |

## 参数

| 参数或选项 | 描述 |
|------------|------|
| `[路径]` | 可选的目标目录；指定后会覆盖当前平台的默认目录。 |
| `--dry-run` | 预览所有待安装、更新、跳过和冲突项，不创建目标目录，也不修改 launcher。 |
| `--force` | 替换冲突的文件或链接；目录永远不会被替换。 |
| `-h`、`--help` | 输出该命令的专用帮助。 |

路径以 `-` 开头时，请在路径前使用 `--`。提供多个目标路径会直接报错，不再静默忽略；`idlebox --install --help` 只显示该命令的帮助，不会执行安装。

## 行为

- 从 Dispatcher 获取完整的 Applet 列表，并在执行任何写入前检查全部目标。
- 若目标目录不存在则自动创建，但 `--dry-run` 不会创建目录。
- 在 Unix-like 系统上创建符号链接。若 launcher 与 `idlebox` 位于同一目录，则使用相对目标；否则使用二进制文件的规范路径。
- 在 Windows 上创建 `<applet>.exe` 硬链接。如果无法创建硬链接（例如跨文件系统），则回退为独占创建的文件副本。
- 已指向当前 IdleBox 二进制文件的 launcher 会被跳过；内容与当前二进制完全相同的 Windows 副本也视为已安装。
- 默认拒绝无关的已有文件和链接。预检发现任意冲突时，会一次性报告所有冲突且不修改任何 launcher。
- 使用 `--force` 可以替换冲突文件或链接，但仍会拒绝并保留目录。
- 每个待安装或更新的 launcher 都会先在目标旁的临时路径创建，再移动到最终位置。
- 输出每个安装或更新操作、实际安装方式（`symbolic link`、`hard link` 或 `copy`）、包含跳过数量的最终汇总，并在需要时提示配置 `PATH`；dry run 会列出全部计划操作。
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
# Done. 36 installed, 0 updated, 0 already installed.

# 安装到自定义目录
idlebox --install ./bin

# 预览安装，不创建 ./bin，也不修改 launcher
idlebox --install --dry-run ./bin

# 明确替换冲突的文件或链接
idlebox --install --force ./bin

# 安装到名称以短横线开头的路径
idlebox --install -- -tools

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
# Done. 36 installed, 0 updated, 0 already installed.

# 安装到自定义目录并直接调用
.\idlebox.exe --install .\bin
.\bin\echo.exe "hello from a launcher"
```

## 注意事项

- Windows 硬链接 launcher 与当前 `idlebox.exe` 共享同一份文件数据，而复制回退得到的是独立快照。替换原始二进制文件后，如果旧副本被报告为冲突，请使用 `--force` 重新安装。
- 重复运行 `--install` 是幂等操作：当前 launcher 会被跳过。仅在确实需要替换其他文件、链接或旧 launcher 时使用 `--force`。
- 预检可以避免已有路径冲突造成的可预见部分安装；后续文件系统或权限错误仍可能在已有 launcher 写入后中止安装，但每个单独替换操作仍采用暂存与可恢复策略。
- 安装完成后，请确保目标目录已加入 `PATH` 环境变量，以便直接通过名称调用 Applet。
- 如需卸载，只需删除目标目录中的 launcher 即可。

## 参见

- [架构概览](../architecture.md)
- [echo](echo.md) · [cat](cat.md) · [ls](ls.md) · [relax](relax.md)
