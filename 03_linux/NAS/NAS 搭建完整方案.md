

---

## **NAS 搭建完整方案**

### **1. 硬件准备**
- **NAS 服务器**：一台电脑（建议至少 4GB 内存）。
- **磁盘**：3 块 1T 硬盘。
- **U 盘**：用于制作 Ubuntu Server 启动盘。
- **网络**：确保 NAS 和客户端设备在同一局域网内。

---

### **2. 安装 Ubuntu Server**
1. **制作启动盘**：
   - 下载 Ubuntu Server 22.04 镜像：[Ubuntu 官网](https://ubuntu.com/download/server)。
   - 使用 [Rufus](https://rufus.ie/) 或 [Balena Etcher](https://www.balena.io/etcher/) 制作启动盘。
2. **安装系统**：
   - 插入启动盘，启动服务器，选择 **Install Ubuntu Server**。
   - 按照向导完成安装：
     - 选择语言、键盘布局。
     - 配置网络（建议使用 DHCP）。
     - 分区时选择 **Use an entire disk**（自动分区）。
     - 设置用户名和密码。
     - 安装 OpenSSH 服务器（方便远程管理）。
3. **更新系统**：
   - 安装完成后，登录系统并更新：
     ```bash
     sudo apt update && sudo apt upgrade -y
     ```

---

### **3. 换源（使用国内镜像源）**
Ubuntu 默认的软件源在国外，下载速度较慢。可以替换为国内镜像源（如阿里云、清华源）。

#### **步骤**：
1. **备份原有源列表**：
   ```bash
   sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
   ```
2. **编辑源列表**：
   ```bash
   sudo nano /etc/apt/sources.list
   ```
3. **替换为阿里云源**：
   - 删除原有内容，替换为以下内容：
     ```bash
     deb http://mirrors.aliyun.com/ubuntu/ jammy main restricted universe multiverse
     deb-src http://mirrors.aliyun.com/ubuntu/ jammy main restricted universe multiverse
     
     deb http://mirrors.aliyun.com/ubuntu/ jammy-security main restricted universe multiverse
     deb-src http://mirrors.aliyun.com/ubuntu/ jammy-security main restricted universe multiverse
     
     deb http://mirrors.aliyun.com/ubuntu/ jammy-updates main restricted universe multiverse
     deb-src http://mirrors.aliyun.com/ubuntu/ jammy-updates main restricted universe multiverse
     
     deb http://mirrors.aliyun.com/ubuntu/ jammy-proposed main restricted universe multiverse
     deb-src http://mirrors.aliyun.com/ubuntu/ jammy-proposed main restricted universe multiverse
     
     deb http://mirrors.aliyun.com/ubuntu/ jammy-backports main restricted universe multiverse
     deb-src http://mirrors.aliyun.com/ubuntu/ jammy-backports main restricted universe multiverse
     ```
4. **更新软件包列表**：
   ```bash
   sudo apt update
   ```

---

### **4. 路由器静态 IP 绑定**
为了避免 NAS 的 IP 地址变化，可以在路由器上为 NAS 绑定静态 IP。

#### **步骤**：
1. **登录路由器管理界面**：
   - 打开浏览器，输入路由器的管理地址（通常是 `192.168.1.1` 或 `192.168.0.1`）。
   - 输入用户名和密码登录（默认信息通常在路由器背面）。
2. **找到 DHCP 静态 IP 绑定设置**：
   - 在路由器的设置菜单中，找到 **DHCP 设置** 或 **局域网设置**。
   - 找到 **静态 IP 绑定** 或 **地址保留** 选项。
3. **绑定 NAS 的 MAC 地址**：
   - 找到 NAS 的 MAC 地址（可以在 NAS 的网络设置中查看，或通过路由器的 DHCP 客户端列表查看）。
   - 将 NAS 的 MAC 地址与一个固定的 IP 地址绑定（例如 `192.168.1.100`）。
4. **保存设置**：
   - 保存配置并重启路由器。
5. **验证静态 IP**：
   - 重启 NAS，检查其 IP 地址是否变为绑定的静态 IP。

---

### **5. 配置磁盘**
1. **查看磁盘信息**：
   - 使用 `lsblk` 命令查看磁盘信息，确认 3 块 1T 磁盘已被识别。
2. **创建 RAID 5 阵列（推荐）**：
   - RAID 5 提供数据冗余和性能提升，使用 3 块磁盘中的 2T 可用空间。
   - 安装 `mdadm` 工具：
     ```bash
     sudo apt install mdadm -y
     ```
   - 创建 RAID 5 阵列：
     ```bash
     sudo mdadm --create --verbose /dev/md0 --level=5 --raid-devices=3 /dev/sdb /dev/sdc /dev/sdd
     ```
   - 格式化 RAID 阵列：
     ```bash
     sudo mkfs.ext4 /dev/md0
     ```
3. **挂载磁盘**：
   - 创建挂载点并挂载 RAID 阵列：
     ```bash
     sudo mkdir /mnt/data
     sudo mount /dev/md0 /mnt/data
     ```
   - 设置开机自动挂载：
     ```bash
     echo '/dev/md0 /mnt/data ext4 defaults 0 0' | sudo tee -a /etc/fstab
     ```

---

### **6. 配置内网穿透（无公网 IP）**
使用 **ZeroTier** 或 **Tailscale** 实现内网穿透，无需公网 IP。

#### **ZeroTier 方案**
1. **注册 ZeroTier**：
   - 访问 [ZeroTier 官网](https://www.zerotier.com/)，注册账号并创建一个网络。
2. **安装 ZeroTier**：
   - 在 NAS 上安装 ZeroTier：
     ```bash
     curl -s https://install.zerotier.com | sudo bash
     ```
   - 加入网络：
     ```bash
     sudo zerotier-cli join <Network-ID>
     ```
3. **授权设备**：
   - 在 ZeroTier 管理界面中，授权 NAS 和客户端设备。
4. **访问 NAS**：
   - 使用 ZeroTier 分配的虚拟 IP 访问 NAS（例如 `192.168.196.x`）。

---

### **7. 配置 Samba 共享**
1. **安装 Samba**：
   - 在 NAS 上安装 Samba：
     ```bash
     sudo apt install samba -y
     ```
2. **配置共享目录**：
   - 编辑 Samba 配置文件：
     ```bash
     sudo nano /etc/samba/smb.conf
     ```
   - 添加以下内容：
     ```ini
     [data]
        path = /mnt/data
        browseable = yes
        writable = yes
        valid users = your_username
     ```
3. **创建 Samba 用户**：
   - 添加 Samba 用户并设置密码：
     ```bash
     sudo smbpasswd -a your_username
     ```
4. **重启 Samba 服务**：
   - 重启 Samba 服务使配置生效：
     ```bash
     sudo systemctl restart smbd
     ```

---

### **8. 访问 NAS**
1. **局域网内访问**：
   - 在客户端设备上，使用文件资源管理器访问：
     - Windows：`\\NAS的IP地址`
     - Linux：`smb://NAS的IP地址`
     - macOS：`smb://NAS的IP地址`
2. **通过内网穿透访问**：
   - 使用 ZeroTier 或 Tailscale 分配的虚拟 IP 或域名访问 NAS。

---

### **总结**
- **换源**：使用国内镜像源（如阿里云）加速软件下载。
- **静态 IP 绑定**：在路由器上为 NAS 绑定静态 IP，避免 IP 变化。
- **磁盘配置**：使用 RAID 5 提供数据冗余和性能提升。
- **内网穿透**：使用 ZeroTier 或 Tailscale 实现无公网 IP 访问。
- **Samba 共享**：配置 Samba 共享，支持多设备访问。

这是完整的 NAS 搭建方案，适合无公网 IP 的用户。如果有其他问题，欢迎随时提问！