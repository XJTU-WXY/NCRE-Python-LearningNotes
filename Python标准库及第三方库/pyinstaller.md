# PyInstaller
## 1. **基本用法**
```bash
pyinstaller [options] script.py
```
`PyInstaller` 的核心任务是将 `script.py` 转换为可执行文件。默认情况下，它会创建一个 `dist/` 目录，其中包含生成的 `.exe` 或 `.app` 文件。

## 2. **打包方式**
| 参数 | 简写 | 作用 |
|------|------|------|
| `--onedir` | `-D` | 生成独立文件夹，包含所有依赖文件（默认方式）。 |
| `--onefile` | `-F` | 生成单个可执行文件，所有依赖被打包到一个 `.exe` 或 `.app` 中。 |
| `--windowed` | `-w` | **（仅 Windows/macOS）** 生成无控制台窗口的 GUI 应用（适用于 PyQt、Tkinter 等 GUI 程序）。 |
| `--console` | `-c` | **（仅 Windows/macOS）** 生成带终端窗口的程序（默认启用）。 |
| `--noconfirm` |  | 覆盖已有的 `build/` 和 `dist/` 目录，无需确认。 |
| `--clean` |  | 清理临时文件，避免缓存影响。 |

## 3. **图标与版本信息**
| 参数 | 简写 | 作用 |
|------|------|------|
| `--icon=icon.ico` | `-i icon.ico` | 指定应用程序的图标（Windows 使用 `.ico`，macOS 使用 `.icns`）。 |
| `--name=appname` | `-n appname` | 指定生成的可执行文件的名称。 |
| `--version-file=file` |  | 指定版本信息（需要 `.txt` 或 `.rc` 资源文件）。 |
| `--upx-dir=UPX_PATH` |  | 指定 `UPX` 压缩工具的路径，用于减少文件大小。 |

## 4. **文件打包**
| 参数 | 简写 | 作用 |
|------|------|------|
| `--add-data "source;dest"` |  | 添加数据文件（Linux/macOS 需用 `:` 代替 `;`）。 |
| `--add-binary "source;dest"` |  | 添加二进制文件。 |
| `--exclude-module module` |  | 排除不必要的模块（如 `matplotlib.tests`）。 |
| `--hidden-import module` |  | 显式指定需要打包的模块（防止 `PyInstaller` 自动分析时遗漏）。 |
| `--collect-data package` |  | 收集某个包的所有数据文件（适用于 `pandas`、`scipy` 等）。 |
| `--collect-binaries package` |  | 收集某个包的所有二进制文件。 |
| `--paths path` | `-p path` | 添加 Python 模块搜索路径。 |

## 5. **高级控制**
| 参数 | 简写 | 作用 |
|------|------|------|
| `--runtime-tmpdir path` |  | 运行时使用的临时目录（仅 `--onefile` 模式下生效）。 |
| `--key=KEY` |  | 对脚本加密，防止被反编译（实验性功能）。 |
| `--log-level LEVEL` |  | 设置日志级别（DEBUG、INFO、WARN、ERROR）。 |
| `--disable-windowed-traceback` |  | **（仅 Windows/macOS）** 关闭 GUI 崩溃时的错误弹窗。 |

## 6. **调试与优化**
| 参数 | 简写 | 作用 |
|------|------|------|
| `--debug` |  | 启用调试模式，打印详细日志。 |
| `--strip` |  | 移除符号表，减少文件大小（Linux/macOS）。 |
| `--noupx` |  | 禁用 `UPX` 压缩。 |
