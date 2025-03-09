# ESP-IDF 多版本环境搭建

如果你也饱受环境折磨，就来看看这个教程吧！

- ## 主题大纲

- 乐鑫官网Docker [介绍](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-guides/tools/idf-docker-image.html)
- docker[镜像拉取](https://hub.docker.com/r/espressif/idf/tags)
- 插件安装ESP-IDF C/C++ Dev Containers remote development
- 命令行 构建Docker Config 文件以及 在容器中运行打开文件夹

![image-20250303082238169](/home/lighting/.config/Typora/typora-user-images/image-20250303082238169.png)

![image-20250303082258799](/home/lighting/.config/Typora/typora-user-images/image-20250303082258799.png)

![](/home/lighting/.config/Typora/typora-user-images/image-20250303082323984.png)

```
{
	// 容器的名称，显示在 VS Code 的 UI 中
	"name": "ESP-IDF",
  
	// 使用的 Docker 镜像名称和标签
	"image": "espressif/idf:v5.1.5",
  
	// 将本地项目目录挂载到容器内的 `/workspaces` 目录
	// ${localWorkspaceFolder} 是 VS Code 提供的变量，表示当前打开的本地项目路径
	"workspaceMount": "source=${localWorkspaceFolder},target=/workspaces,type=bind",
  
	// 容器启动后的默认工作目录
	// 这里设置为 `/workspaces`，表示容器启动后会直接进入该目录
	"workspaceFolder": "/workspaces",
  
	// 挂载配置：将 VS Code 扩展缓存挂载到容器内
	// 避免每次重建容器时重新下载扩展
	"mounts": [
	  "source=extensionCache,target=/root/.vscode-server/extensions,type=volume"
	],
  
	// 将配置插件的相关参数传递到容器中
	"settings": {
	  // 设置默认的终端配置文件为 Bash
	  "terminal.integrated.defaultProfile.linux": "bash",
  
	  // ESP-IDF 相关配置
	  "idf.espIdfPath": "/opt/esp/idf",          // ESP-IDF 的安装路径
	  "idf.customExtraPaths": "",                // 自定义额外路径
	  "idf.pythonBinPath": "/opt/esp/python_env/idf5.0_py3.8_env/bin/python",  // Python 解释器路径
	  "idf.toolsPath": "/opt/esp",               // 工具路径
	  "idf.gitPath": "/usr/bin/git"              // Git 路径
	},
  
	// 容器创建时需要安装的 VS Code 扩展
	"extensions": [
	  "ms-vscode.cpptools",                      // C/C++ 开发工具
	  "espressif.esp-idf-extension"              // ESP-IDF 官方扩展
	],
  
	// 容器运行时的额外参数
	"runArgs": [
	  "--privileged"                          // 以特权模式运行容器，以便访问 USB 设备                      // 设置容器内的用户 ID 和组 ID（替换为你的用户ID和组ID）
	]
  }
```

```
# 使用 ESP-IDF 官方镜像作为基础镜像
FROM espressif/idf:v5.1.5

# 设置非交互模式
ARG DEBIAN_FRONTEND=nointeractive

# 设置环境变量
ENV IDF_PATH=/opt/esp/idf
ENV HOME=/root

# 初始化 ESP-IDF 环境
RUN echo $($IDF_PATH/tools/idf_tools.py export) >> $HOME/.bashrc

# 安装 idf-component-manager
RUN pip install --no-cache-dir idf-component-manager

# 设置入口点
ENTRYPOINT ["/opt/esp/entrypoint.sh"]
CMD ["/bin/bash"]
```

![image-20250303082430566](/home/lighting/.config/Typora/typora-user-images/image-20250303082430566.png)

![image-20250303083300490](/home/lighting/.config/Typora/typora-user-images/image-20250303083300490.png)





为了在 **Ubuntu 系统** 上搭建 **ESP-IDF 多版本开发环境**，你可以结合 Docker 和 VS Code 的 Dev Containers 插件来实现。以下是详细的补充内容，帮助你完成环境搭建。

---

## 1. **准备工作**
在开始之前，确保你的 Ubuntu 系统已经安装了以下工具：
- **Docker**：用于运行 ESP-IDF 的官方镜像。
- **VS Code**：用于开发和调试。
- **VS Code 插件**：安装 `Dev Containers` 和 `ESP-IDF` 插件。

### 1.1 安装 Docker
在 Ubuntu 上安装 Docker：
```bash
sudo apt update
sudo apt install docker.io
sudo systemctl start docker
sudo systemctl enable docker
```
将当前用户添加到 `docker` 组，避免每次使用 `sudo`：
```bash
sudo usermod -aG docker $USER
newgrp docker
```

### 1.2 安装 VS Code
从 [VS Code 官网](https://code.visualstudio.com/) 下载并安装 VS Code。

### 1.3 安装 VS Code 插件
打开 VS Code，安装以下插件：
- **Dev Containers**：用于在容器中开发。
- **ESP-IDF**：用于 ESP-IDF 项目的开发支持。

---

## 2. **拉取 ESP-IDF Docker 镜像**
乐鑫提供了官方的 ESP-IDF Docker 镜像，支持多个版本。你可以根据需要拉取特定版本的镜像。

### 2.1 拉取镜像
例如，拉取 ESP-IDF v5.1.5 镜像：
```bash
docker pull espressif/idf:v5.1.5
```

### 2.2 查看可用镜像
你可以在 [Docker Hub](https://hub.docker.com/r/espressif/idf/tags) 上查看所有可用的 ESP-IDF 镜像版本。

---

## 3. **配置 Dev Containers**
使用 VS Code 的 Dev Containers 插件，可以方便地在容器中开发 ESP-IDF 项目。

### 3.1 创建 `.devcontainer` 文件夹

安装完成ESP-IDF插件之后，按下键盘 F1键，并且选择

![image-20250304092233113](/home/lighting/.config/Typora/typora-user-images/image-20250304092233113.png)

### 3.2 配置 `devcontainer.json`
以下是一个示例配置文件：
```json
{
	// 容器的名称，显示在 VS Code 的 UI 中
	"name": "ESP-IDF",
  
	// 使用的 Docker 镜像名称和标签
	"image": "espressif/idf:v5.1.5",
  
	// 将本地项目目录挂载到容器内的 `/workspaces` 目录
	// ${localWorkspaceFolder} 是 VS Code 提供的变量，表示当前打开的本地项目路径
	"workspaceMount": "source=${localWorkspaceFolder},target=/workspaces,type=bind",
  
	// 容器启动后的默认工作目录
	// 这里设置为 `/workspaces`，表示容器启动后会直接进入该目录
	"workspaceFolder": "/workspaces",
  
	// 挂载配置：将 VS Code 扩展缓存挂载到容器内
	// 避免每次重建容器时重新下载扩展
	"mounts": [
	  "source=extensionCache,target=/root/.vscode-server/extensions,type=volume"
	],
  
	// 将配置插件的相关参数传递到容器中
	"settings": {
	  // 设置默认的终端配置文件为 Bash
	  "terminal.integrated.defaultProfile.linux": "bash",
  
	  // ESP-IDF 相关配置
	  "idf.espIdfPath": "/opt/esp/idf",          // ESP-IDF 的安装路径
	  "idf.customExtraPaths": "",                // 自定义额外路径
	  "idf.pythonBinPath": "/opt/esp/python_env/idf5.0_py3.8_env/bin/python",  // Python 解释器路径
	  "idf.toolsPath": "/opt/esp",               // 工具路径
	  "idf.gitPath": "/usr/bin/git"              // Git 路径
	},
  
	// 容器创建时需要安装的 VS Code 扩展
	"extensions": [
	  "ms-vscode.cpptools",                      // C/C++ 开发工具
	  "espressif.esp-idf-extension"              // ESP-IDF 官方扩展
	],
  
	// 容器运行时的额外参数
	"runArgs": [
	  "--privileged"                          // 以特权模式运行容器，以便访问 USB 设备                      // 设置容器内的用户 ID 和组 ID（替换为你的用户ID和组ID）
	]
  }
```

### 3.3 配置 `Dockerfile`（可选）
如果你需要自定义容器镜像，可以创建 `Dockerfile`：
```dockerfile
FROM espressif/idf:v5.1.5

ARG DEBIAN_FRONTEND=nointeractive

ENV IDF_PATH=/opt/esp/idf
ENV HOME=/root

RUN echo $($IDF_PATH/tools/idf_tools.py export) >> $HOME/.bashrc

RUN pip install --no-cache-dir idf-component-manager

ENTRYPOINT ["/opt/esp/entrypoint.sh"]
CMD ["/bin/bash"]
```

---

## 4. **启动 Dev Container**
1. 打开 VS Code。
2. 按下 `Ctrl+Shift+P`，输入 `Dev Containers: Reopen in Container`，选择你的项目文件夹。
3. VS Code 会自动构建并启动容器。

---

## 5. **验证环境**
在容器中打开终端，运行以下命令验证 ESP-IDF 环境是否正常：
```bash
idf.py --version
```
如果输出了 ESP-IDF 的版本信息，说明环境配置成功。

---

## 6. **多版本管理**
如果你需要同时使用多个 ESP-IDF 版本，可以通过以下方式实现：
1. 为每个项目创建独立的 `.devcontainer` 文件夹，并指定不同的镜像版本。
2. 使用 `idf.py set-target` 命令切换目标芯片（如 ESP32、ESP32-C3 等）。

---

## 7. **常见问题**
### 7.1 容器无法访问 USB 设备
确保容器以 `--privileged` 模式运行，并挂载 USB 设备：
```json
"runArgs": [
  "--privileged",
  "--device=/dev/ttyUSB0"
]
```

### 7.2 容器内无法使用 Git
确保容器内安装了 Git：
```dockerfile
RUN apt update && apt install -y git
```

### 7.3 扩展缓存问题
如果扩展缓存挂载失败，可以手动安装扩展：
```bash
code --install-extension ms-vscode.cpptools
code --install-extension espressif.esp-idf-extension
```

---

## 8. **总结**
通过 Docker 和 Dev Containers，你可以在 Ubuntu 系统上轻松搭建 ESP-IDF 多版本开发环境。这种方法不仅隔离了不同版本的环境，还简化了配置过程。如果你有更多问题，可以参考 [乐鑫官方文档](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-guides/tools/idf-docker-image.html)。