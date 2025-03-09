### **📦 完整的 Ubuntu NAS 方案（功能全面，支持手机 & 电脑）**

✅ **文件存储 & 远程访问**（支持 SMB / WebDAV / SFTP）
 ✅ **多设备同步**（Nextcloud / Syncthing）
 ✅ **AI 照片管理**（PhotoPrism）
 ✅ **流媒体播放**（Jellyfin / Plex）
 ✅ **BT / PT 下载**（qBittorrent / Aria2）
 ✅ **低功耗 & 安全优化**（ZFS / Btrfs / Tailscale VPN）

------

## **📌 1. 硬件 & 系统准备**

### **🔹 推荐硬件**

| 需求           | 推荐配置                                 |
| -------------- | ---------------------------------------- |
| **低功耗 NAS** | Intel N100 / J6412 迷你主机 + 2-4 盘位   |
| **性能 NAS**   | i3 / i5 低功耗平台 + ITX 主板 + 4-6 盘位 |
| **高性能 NAS** | 二手 E3 / E5 至强服务器（适合 RAID）     |

✅ 硬盘建议：

- **系统盘**：SSD 128GB 以上（Ubuntu + Docker 运行）
- **数据盘**：HDD / SSD（建议用 **ZFS / Btrfs** 管理存储）

------

### **🔹 安装 Ubuntu**

1. 下载 

   Ubuntu Server 22.04 LTS

   - 官网：https://ubuntu.com/download/server

2. 安装时选择：

   - **最低安装**（Minimal）
   - **开启 SSH 远程管理**

💡 **安装完毕后，推荐使用 SSH 远程管理：**

```bash
ssh username@NAS_IP
```

------

## **📌 2. 安装基础软件**

### **🔹 更新系统**

```bash
sudo apt update && sudo apt upgrade -y
```

### **🔹 安装基本工具**

```bash
sudo apt install -y htop vim curl wget git net-tools
```

### **🔹 安装 Docker（核心应用管理）**

```bash
sudo apt install -y docker docker-compose
sudo systemctl enable --now docker
```

💡 **Docker 让你可以轻松安装 NAS 各种应用！**

------

## **📌 3. 存储管理（ZFS / Btrfs）**

如果你希望 **高效存储 & 数据保护**，推荐 **ZFS 或 Btrfs**：

```bash
sudo apt install -y zfsutils-linux
```

💡 **ZFS 支持快照、RAID，适合数据安全需求**。

------

## **📌 4. 文件共享 & 远程访问**

### **🔹 安装 SMB（Windows & macOS 共享）**

```bash
sudo apt install -y samba
```

配置 `/etc/samba/smb.conf`：

```ini
[shared]
   path = /mnt/data
   read only = no
   browsable = yes
   guest ok = no
   create mask = 0777
   directory mask = 0777
```

重启 Samba：

```bash
sudo systemctl restart smbd
```

### **🔹 远程访问（无公网 IP 也能访问）**

✅ **Tailscale VPN**（最简单的远程访问方案）：

```bash
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up
```

💡 **手机 & 电脑安装 Tailscale 后，即可访问 NAS！**

------

## **📌 5. 文件同步 & 备份**

### **🔹 Nextcloud（私有云盘）**

```bash
docker run -d --name nextcloud -p 8080:80 -v /mnt/data/nextcloud:/var/www/html nextcloud
```

访问 `http://NAS_IP:8080`，配置 **私人网盘**。

### **🔹 Syncthing（自动文件同步）**

```bash
docker run -d --name syncthing -p 8384:8384 -v /mnt/data:/var/syncthing syncthing/syncthing
```

💡 **支持 Android、Windows、Mac 设备自动同步文件！**

------

## **📌 6. AI 照片管理（PhotoPrism）**

```bash
docker run -d --name photoprism -p 2342:2342 -v /mnt/photos:/photoprism photoprism/photoprism
```

访问 `http://NAS_IP:2342`，开始智能相册管理！🚀

------

## **📌 7. 流媒体中心**

### **🔹 Jellyfin（家庭影院）**

```bash
docker run -d --name jellyfin -p 8096:8096 -v /mnt/media:/media jellyfin/jellyfin
```

访问 `http://NAS_IP:8096`，可直接播放 NAS 里的电影！🍿

------

## **📌 8. 下载管理**

### **🔹 qBittorrent（BT & PT 下载）**

```bash
docker run -d --name qbittorrent -p 8081:8080 -v /mnt/downloads:/downloads linuxserver/qbittorrent
```

访问 `http://NAS_IP:8081`，支持种子 & 磁力下载！⚡

------

## **📌 9. 进阶优化**

✅ **启用 BBR（加速网络访问）：**

```bash
echo "net.core.default_qdisc=fq" | sudo tee -a /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

✅ **定期更新 Docker 容器：**

```bash
docker ps -q | xargs docker pull
```

✅ **远程管理 NAS（Web 界面管理）：**

```bash
docker run -d --name portainer -p 9000:9000 portainer/portainer-ce
```

💡 **访问 `http://NAS_IP:9000`，可以通过网页管理 Docker 应用！**

------

## **🎯 结论：完整 Ubuntu NAS 方案**

| **功能**        | **解决方案**                      |
| --------------- | --------------------------------- |
| **文件共享**    | SMB / WebDAV / SFTP               |
| **远程访问**    | Tailscale VPN / Cloudflare Tunnel |
| **文件同步**    | Nextcloud / Syncthing             |
| **照片管理**    | PhotoPrism（AI 自动分类）         |
| **电影 & 音乐** | Jellyfin / Plex                   |
| **下载管理**    | qBittorrent / Aria2               |
| **系统管理**    | Docker + Portainer                |

------

## **🚀 你的 NAS 计划**

💡 这个方案 **功能非常全面**，手机 & 电脑都能使用！你更关注 **哪些功能**？
 需要更详细的 **安装教程** 或 **远程访问方案** 吗？😊