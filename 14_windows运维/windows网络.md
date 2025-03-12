# Windows 网络命令终极扩展版

## 一、基础网络诊断命令

| 命令       | 功能               | 示例                                                         |
| ---------- | ------------------ | ------------------------------------------------------------ |
| `ipconfig` | 显示/刷新IP配置    | `ipconfig /all`（完整信息）<br>`ipconfig /release`（释放IP）<br>`ipconfig /renew`（续订IP） |
| `ping`     | 测试网络连通性     | `ping -t 8.8.8.8`（持续ping）<br>`ping -n 10 www.baidu.com`（指定次数） |
| `tracert`  | 路由跟踪（按跳数） | `tracert -d 8.8.8.8`（禁用DNS解析，加速）                    |
| `pathping` | 综合路由+丢包统计  | `pathping -n 8.8.8.8`（跳过DNS解析）                         |
| `netstat`  | 查看网络连接状态   | `netstat -ano | findstr "ESTABLISHED"`（筛选活动连接）<br>`netstat -b`（显示占用端口的进程） |
| `nslookup` | DNS解析与故障排查  | `nslookup -type=MX example.com`（查询邮件服务器记录）        |
| `arp`      | 管理ARP缓存        | `arp -a`（显示ARP表）<br>`arp -d *`（清除所有ARP缓存）       |
| `route`    | 路由表管理         | `route print`（显示路由表）<br>`route add 192.168.2.0 mask 255.255.255.0 192.168.1.1`（添加静态路由） |

## 二、网络配置与接口管理

| 命令       | 功能                 | 深度用法                                                     |
| ---------- | -------------------- | ------------------------------------------------------------ |
| `netsh`    | 网络配置的瑞士军刀   | 1. **重置网络适配器**：<br>`netsh int ip reset reset.log`<br>2. **导出/导入配置**：<br>`netsh dump > config.txt`<br>`netsh exec config.txt`<br>3. **设置静态IP**：<br>`netsh interface ip set address "以太网" static 192.168.1.100 255.255.255.0 192.168.1.1` |
| `wmic`     | 查询硬件与网络信息   | `wmic nic where "NetEnabled=true" get name, speed`（查看启用网卡的名称和速度） |
| `getmac`   | 获取MAC地址          | `getmac /v /fo list`（详细列表格式）                         |
| `ncpa.cpl` | 快速打开网络连接面板 | 直接运行 `ncpa.cpl`（无需命令参数）                          |

## 三、端口与协议分析

| 命令                 | 场景                           | 高级技巧                                                     |
| -------------------- | ------------------------------ | ------------------------------------------------------------ |
| `telnet`             | 测试远程端口连通性             | `telnet 192.168.1.1 80`（若返回空白，80端口开放）            |
| `Test-NetConnection` | PowerShell端口检测             | `Test-NetConnection -ComputerName google.com -Port 443 -InformationLevel Detailed`（详细结果） |
| `curl`               | HTTP请求与API测试              | `curl -v -X POST -H "Content-Type: application/json" -d '{"key":"value"}' http://api.example.com` |
| `PortQry`            | 微软官方端口扫描工具（需下载） | `PortQry.exe -n 192.168.1.1 -e 80`（检测端口状态）           |

## 四、远程管理与服务

| 命令    | 用途                        | 关键操作                                                     |
| ------- | --------------------------- | ------------------------------------------------------------ |
| `ssh`   | 远程连接Linux/Windows服务器 | `ssh -i key.pem user@ec2-1-2-3-4.compute-1.amazonaws.com`（使用密钥登录AWS） |
| `scp`   | 安全文件传输                | `scp -r C:\Folder user@remote:/path`（递归上传文件夹）       |
| `mstsc` | 远程桌面连接                | `mstsc /v:192.168.1.100 /admin`（以管理员模式连接）          |
| `net`   | 管理共享与用户              | `net share`（查看共享资源）<br>`net use Z: \\192.168.1.100\share /user:admin password`（映射网络驱动器） |

## 五、防火墙与安全

| 命令                | 功能              | 示例                                                         |
| ------------------- | ----------------- | ------------------------------------------------------------ |
| `netsh advfirewall` | 高级防火墙配置    | 1. 允许端口：<br>`netsh advfirewall firewall add rule name="Open Port 80" dir=in action=allow protocol=TCP localport=80`<br>2. 导出规则：<br>`netsh advfirewall export "C:\firewall.xml"` |
| `wf.msc`            | 打开防火墙高级GUI | 直接运行 `wf.msc`                                            |
| `auditpol`          | 审计策略管理      | `auditpol /get /category:*`（查看所有审计策略）              |

## 六、DNS与组策略

| 命令       | 场景                           | 命令示例                                                |
| ---------- | ------------------------------ | ------------------------------------------------------- |
| `dnscmd`   | DNS服务器管理（需安装DNS服务） | `dnscmd /zoneadd example.com /Primary`（创建主DNS区域） |
| `gpresult` | 查看组策略应用结果             | `gpresult /h report.html`（生成HTML报告）               |
| `gpupdate` | 强制刷新组策略                 | `gpupdate /force`（立即生效）                           |

## 七、系统日志与监控

| 工具           | 用途                       | 操作指南                                                     |
| -------------- | -------------------------- | ------------------------------------------------------------ |
| `eventvwr.msc` | 事件查看器（网络相关日志） | 筛选 Windows日志 -> 系统，搜索来源为 Tcpip 或 Dhcp-Client 的事件 |
| `perfmon`      | 性能监视器（网络流量监控） | 添加计数器：Network Interface -> Bytes Total/sec             |
| `resmon`       | 资源监视器（实时网络活动） | 直接运行 `resmon`，切换到“网络”标签                          |

## 八、第三方工具推荐

1. **Wireshark**：抓包分析（需安装）  

   ```bash
   wireshark -k -i "以太网" -Y "http"  # 捕获HTTP流量
   ```

2. **Nmap**：端口扫描与网络探测  

   ```bash
   nmap -sS -T4 192.168.1.0/24  # 快速扫描局域网活跃主机
   ```

3. **Sysinternals Suite**（微软官方工具集）：  

   - TCPView：图形化查看TCP/UDP连接  
   - PsPing：高级ICMP/TCP延迟测试  

## 九、PowerShell 专属命令

| Cmdlet               | 功能           | 示例                                                         |
| -------------------- | -------------- | ------------------------------------------------------------ |
| `Get-NetAdapter`     | 获取网卡信息   | `Get-NetAdapter | Where-Object { $_.Status -eq 'Up' }`（筛选启用的网卡） |
| `Test-NetRoute`      | 测试路由可达性 | `Test-NetRoute -DestinationPrefix 8.8.8.8`                   |
| `Start-BitsTransfer` | 后台文件传输   | `Start-BitsTransfer -Source http://example.com/file.zip -Destination C:\Downloads` |

## 十、实战场景示例

### 场景1：排查DNS问题

```cmd
nslookup www.google.com 8.8.8.8  # 指定DNS服务器查询
ipconfig /flushdns                # 清除本地DNS缓存
```

### 场景2：监控异常外联

```cmd
netstat -ano | findstr "ESTABLISHED"  # 查看所有活动连接
tasklist | findstr "1234"             # 根据PID查找进程名
```

### 场景3：批量配置多台设备IP

```powershell
# PowerShell脚本示例（需管理员权限）
$adapters = Get-NetAdapter -Name "以太网*"
foreach ($adapter in $adapters) {
    New-NetIPAddress -InterfaceIndex $adapter.ifIndex -IPAddress 192.168.1.100 -PrefixLength 24 -DefaultGateway 192.168.1.1
    Set-DnsClientServerAddress -InterfaceIndex $adapter.ifIndex -ServerAddresses ("8.8.8.8", "8.8.4.4")
}
```

## 十一、网络性能优化与监控

| 命令         | 功能                         | 示例                                                         |
| ------------ | ---------------------------- | ------------------------------------------------------------ |
| `typeperf`   | 监控网络性能计数器           | `typeperf "\Network Interface(*)\Bytes Total/sec" -o perfmon.csv`（将网络接口的字节总数/秒数据输出到CSV文件） |
| `perfmon`    | 性能监视器                   | 添加计数器：Network Interface -> Bytes Total/sec             |
| `netstat -e` | 显示网络接口的以太网统计信息 | `netstat -e`（显示发送和接收的字节数、数据包数等）           |

## 十二、网络安全与审计

| 命令                        | 功能                                      | 示例                                                         |
| --------------------------- | ----------------------------------------- | ------------------------------------------------------------ |
| `netsh advfirewall monitor` | 监控防火墙规则的匹配情况                  | `netsh advfirewall monitor show rule name=all`（显示所有防火墙规则的匹配情况） |
| `icacls`                    | 查看和修改文件和目录的访问控制列表（ACL） | `icacls C:\Folder`（显示C:\Folder的ACL）<br>`icacls C:\Folder /grant:r User:(F)`（授予用户对C:\Folder的完全控制权限） |
| `wevtutil`                  | 事件日志实用工具                          | `wevtutil qe System /q:"*[System[Provider[@name='Tcpip']]]"`（查询系统日志中所有来自Tcpip提供程序的事件） |

## 十三、网络自动化与脚本

| 命令       | 功能               | 示例                                                         |
| ---------- | ------------------ | ------------------------------------------------------------ |
| `for /f`   | 批量处理网络信息   | `for /f "tokens=2" %i in ('arp -a') do @echo %i`（提取ARP表中的IP地址） |
| `schtasks` | 创建和管理计划任务 | `schtasks /create /tn "NetworkMonitor" /tr "ping -n 10 8.8.8.8 > ping.log" /sc daily /st 00:00`（创建一个每天午夜执行的计划任务，ping 8.8.8.8十次并将结果保存到ping.log） |

## 十四、无线网络管理

| 命令             | 功能                       | 示例                                                         |
| ---------------- | -------------------------- | ------------------------------------------------------------ |
| `netsh wlan`     | 管理无线网络连接           | `netsh wlan show networks`（显示可用的无线网络）<br>`netsh wlan connect name="MyWiFi"`（连接到名为MyWiFi的无线网络） |
| `wmic nicconfig` | 获取无线网络接口的详细信息 | `wmic nicconfig where "Description like '%Wireless%'" get SSID, SignalStrength`（显示无线网络接口的SSID和信号强度） |

## 十五、虚拟网络与云服务

| 命令                        | 功能           | 示例                                                         |
| --------------------------- | -------------- | ------------------------------------------------------------ |
| `netsh interface portproxy` | 配置端口转发   | `netsh interface portproxy add v4tov4 listenport=80 connectaddress=192.168.1.100 connectport=80`（将本地80端口的流量转发到192.168.1.100的80端口） |
| `awscli` / `azcli`          | 管理云网络资源 | `aws ec2 describe-vpcs`（列出AWS账户中的所有VPC）<br>`az network vnet list`（列出Azure订阅中的所有虚拟网络） |

## 十六、国际化的网络命令

| 命令     | 功能                       | 示例                                                         |
| -------- | -------------------------- | ------------------------------------------------------------ |
| `locale` | 查看和设置系统的区域信息   | `locale`（显示当前区域信息）<br>`locale -a`（显示支持的区域设置） |
| `chcp`   | 更改命令提示符的字符编码页 | `chcp 65001`（设置编码为UTF-8）                              |

## 十七、网络命令的组合使用

| 组合            | 功能                                 | 示例                                                         |
| --------------- | ------------------------------------ | ------------------------------------------------------------ |
| `|`（管道符号） | 将一个命令的输出作为另一个命令的输入 | `ping -n 10 8.8.8.8 | find "TTL="`（提取ping命令输出中包含TTL=的部分） |
| `>`和`>>`       | 将命令输出保存到文件中               | `netstat -ano > netstat.log`（将netstat的输出保存到netstat.log）<br>`ipconfig /all >> network_info.txt`（将ipconfig的输出追加到network_info.txt） |

## 十八、网络命令的错误处理

| 命令         | 功能                                         | 示例                                                    |
| ------------ | -------------------------------------------- | ------------------------------------------------------- |
| `errorlevel` | 在批处理脚本中，根据命令的返回值进行错误处理 | `ping 8.8.8.8`<br>`if %errorlevel% neq 0 echo Ping失败` |
| `timeout`    | 在网络命令执行之间添加延迟                   | `timeout /t 30`（等待30秒）                             |

## 十九、网络命令的可视化展示

| 命令       | 功能           | 示例                                                         |
| ---------- | -------------- | ------------------------------------------------------------ |
| `start`    | 打开图形化工具 | `start http://example.com`（在默认浏览器中打开example.com）  |
| `msconfig` | 系统配置工具   | `msconfig`（打开系统配置界面，可以查看和管理网络启动项和服务） |

## 二十、网络命令的文档与帮助

| 命令                | 功能                     | 示例                                                |
| ------------------- | ------------------------ | --------------------------------------------------- |
| `/help`或`/?`       | 显示命令的帮助信息       | `ipconfig /?`（显示ipconfig的详细帮助）             |
| `echo %errorlevel%` | 检查上一个命令的执行状态 | `echo %errorlevel%`（在脚本中检查命令是否成功执行） |

