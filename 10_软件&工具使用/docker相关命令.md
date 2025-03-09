Docker 是一个开源的应用容器引擎，允许开发者将应用及其依赖打包到一个轻量级、可移植的容器中。以下是一些常用的 Docker 命令：

### 镜像相关命令
1. **搜索镜像**：
   ```bash
   docker search <镜像名>
   ```

2. **拉取镜像**：
   ```bash
   docker pull <镜像名>:<标签>
   ```

3. **列出本地镜像**：
   ```bash
   docker images
   ```

4. **删除本地镜像**：
   ```bash
   docker rmi <镜像ID或镜像名>
   ```

5. **构建镜像**：
   ```bash
   docker build -t <镜像名>:<标签> <Dockerfile路径>
   ```

### 容器相关命令
1. **运行容器**：
   ```bash
   docker run [选项] <镜像名> [命令]
   ```
   常用选项：
   - `-d`：后台运行
   - `-p`：端口映射（主机端口:容器端口）
   - `-v`：卷挂载（主机目录:容器目录）
   - `--name`：指定容器名称
   - `-e`：设置环境变量

2. **列出运行中的容器**：
   ```bash
   docker ps
   ```

3. **列出所有容器（包括停止的）**：
   ```bash
   docker ps -a
   ```

4. **启动容器**：
   ```bash
   docker start <容器ID或容器名>
   ```

5. **停止容器**：
   ```bash
   docker stop <容器ID或容器名>
   ```

6. **重启容器**：
   ```bash
   docker restart <容器ID或容器名>
   ```

7. **进入容器**：
   ```bash
   docker exec -it <容器ID或容器名> /bin/bash
   ```

8. **查看容器日志**：
   ```bash
   docker logs <容器ID或容器名>
   ```

9. **删除容器**：
   ```bash
   docker rm <容器ID或容器名>
   ```

10. **强制删除运行中的容器**：
    ```bash
    docker rm -f <容器ID或容器名>
    ```

### 网络相关命令
1. **列出网络**：
   ```bash
   docker network ls
   ```

2. **创建网络**：
   ```bash
   docker network create <网络名>
   ```

3. **查看网络详情**：
   ```bash
   docker network inspect <网络名>
   ```

4. **删除网络**：
   ```bash
   docker network rm <网络名>
   ```

### 卷相关命令
1. **列出卷**：
   ```bash
   docker volume ls
   ```

2. **创建卷**：
   ```bash
   docker volume create <卷名>
   ```

3. **查看卷详情**：
   ```bash
   docker volume inspect <卷名>
   ```

4. **删除卷**：
   ```bash
   docker volume rm <卷名>
   ```

### 系统相关命令
1. **查看 Docker 系统信息**：
   ```bash
   docker info
   ```

2. **查看 Docker 版本**：
   ```bash
   docker version
   ```

3. **清理未使用的镜像、容器、卷和网络**：
   ```bash
   docker system prune
   ```

4. **清理所有未使用的资源（包括未使用的镜像）**：
   ```bash
   docker system prune -a
   ```

### 其他常用命令
1. **查看容器资源使用情况**：
   ```bash
   docker stats <容器ID或容器名>
   ```

2. **复制文件到容器**：
   
   ```bash
   docker cp <本地文件路径> <容器ID或容器名>:<容器内路径>
   ```
   
3. **从容器复制文件到本地**：
   ```bash
   docker cp <容器ID或容器名>:<容器内路径> <本地文件路径>
   ```

4. **查看容器进程**：
   ```bash
   docker top <容器ID或容器名>
   ```

5. **提交容器为镜像**：
   ```bash
   docker commit <容器ID或容器名> <新镜像名>:<标签>
   ```

这些命令涵盖了 Docker 的日常使用场景，帮助你高效地管理和操作 Docker 容器和镜像。