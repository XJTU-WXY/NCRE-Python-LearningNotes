# PyPI
`pip`（Python Package Installer）是 Python 官方推荐的包管理工具，负责安装、管理、卸载 Python 包，并支持环境管理、包信息查询等功能。以下是 `pip` 的所有相关命令及其详细用法，包括环境管理、包管理、分发文件处理等方面。

# **1. 环境管理与自省**
这些命令用于管理 Python 环境中已安装的包，并检查其状态。

## **1.1 安装 Python 包**
```sh
pip install package_name
```
**选项：**
- `pip install package_name==1.2.3`  → 安装指定版本  
- `pip install package_name>=1.2.0,<2.0`  → 安装符合版本范围的包  
- `pip install --upgrade package_name`  → 更新已安装的包  
- `pip install --no-cache-dir package_name`  → 禁用缓存安装  

**示例：**
```sh
pip install numpy
pip install requests==2.28.0
pip install pandas --upgrade
```

## **1.2 卸载 Python 包**
```sh
pip uninstall package_name
```
**示例：**
```sh
pip uninstall flask
```
> 使用 `-y` 可跳过确认：
```sh
pip uninstall -y flask
```

## **1.3 检查环境和包信息**
### **1.3.1 `pip inspect`（检查 pip 依赖信息）**
```sh
pip inspect
```
此命令会显示当前环境的依赖树、包冲突等信息（`pip 23.1` 及以上版本支持）。

## **1.4 列出已安装的包**
```sh
pip list
```
**选项：**
- `pip list --outdated` → 列出可升级的包  
- `pip list --format=freeze` → 以 `requirements.txt` 格式显示包  
- `pip list --not-required` → 显示没有其他包依赖的包  

**示例：**
```sh
pip list --outdated
```


## **1.5 显示特定包的信息**
```sh
pip show package_name
```
**示例：**
```sh
pip show numpy
```
**示例输出：**
```
Name: numpy
Version: 1.23.0
Summary: Fundamental package for array computing with Python.
Home-page: https://numpy.org/
Location: /usr/local/lib/python3.10/site-packages
```

## **1.6 冻结当前环境的依赖**
```sh
pip freeze
```
**示例：**
```sh
pip freeze > requirements.txt
```
然后在另一环境中恢复：
```sh
pip install -r requirements.txt
```

## **1.7 检查已安装包的依赖是否有问题**
```sh
pip check
```
此命令会检查是否存在缺失的依赖或不兼容的版本。

**示例：**
```sh
pip check
```
**可能输出：**
```
requests 2.28.0 requires urllib3<1.27,>=1.21.1, but you have urllib3 2.0.0.
```

# **2. 处理分发文件**
这些命令用于下载包、生成 `.whl` 文件以及计算包的哈希值。

## **2.1 下载但不安装包**
```sh
pip download package_name
```
**示例：**
```sh
pip download scipy
```
这将在当前目录下载 `scipy` 的 `.whl` 文件。

## **2.2 生成 `.whl` 安装文件**
```sh
pip wheel package_name
```
`wheel` 是 Python 包的二进制分发格式，适用于加快安装速度。

**示例：**
```sh
pip wheel requests
```
这将在当前目录生成 `requests-*.whl` 文件。

## **2.3 计算包文件的哈希值**
```sh
pip hash filename
```
用于验证 `.whl` 或 `.tar.gz` 文件的完整性。

**示例：**
```sh
pip hash numpy-1.23.0-cp310-cp310-win_amd64.whl
```

# **3. PyPI 相关信息**
这些命令用于搜索 PyPI 上的包信息。

## **3.1 搜索 PyPI 上的包**
```sh
pip search package_name
```
**⚠️ 注意**：`pip search` **已被 PyPI 停用**，可以改用：
```sh
https://pypi.org/search/
```


# **4. 管理 `pip` 本身）**
这些命令用于管理 `pip` 的缓存、配置以及调试信息。

## **4.1 管理 `pip` 缓存**
### **4.1.1 查看缓存目录**
```sh
pip cache dir
```
**示例输出：**
```
~/.cache/pip
```

### **4.1.2 清理 `pip` 缓存**
```sh
pip cache purge
```
或仅清理特定包：
```sh
pip cache remove package_name
```

## **4.2 配置 `pip`**
### **4.2.1 查看当前 `pip` 配置**
```sh
pip config list
```
### **4.2.2 设置 PyPI 镜像源**
```sh
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```
**常见国内镜像：**
| 镜像源         | 地址 |
|--------------|---------------------------------|
| 清华大学 TUNA | `https://pypi.tuna.tsinghua.edu.cn/simple` |
| 阿里云       | `https://mirrors.aliyun.com/pypi/simple/` |

### **4.2.3 取消某个配置**
```sh
pip config unset global.index-url
```

## **4.3 调试 `pip`**
### **4.3.1 查看 `pip` 详细信息**
```sh
pip debug
```
示例输出：
```
pip version: 23.0.1
Python version: 3.10.8
OS: Linux-5.15.0-52-generic-x86_64
```

### **4.3.2 调试 `pip` 过程**
```sh
pip install package_name -v
```
或：
```sh
pip install package_name --log pip.log
```

# **总结**
| 命令 | 作用 |
|------|------|
| `pip install package` | 安装包 |
| `pip uninstall package` | 卸载包 |
| `pip inspect` | 检查依赖信息 |
| `pip list` | 列出已安装包 |
| `pip show package` | 显示包详细信息 |
| `pip freeze` | 记录当前环境依赖 |
| `pip check` | 检查依赖问题 |
| `pip download package` | 下载包但不安装 |
| `pip wheel package` | 生成 `.whl` 文件 |
| `pip hash file` | 计算文件哈希值 |
| `pip search package` | 在 PyPI 搜索包（已停用） |
| `pip cache dir` | 显示缓存目录 |
| `pip cache purge` | 清理 `pip` 缓存 |
| `pip config set` | 配置 `pip` |
| `pip debug` | 调试 `pip` |
| `pip install -v` | 详细日志模式 |