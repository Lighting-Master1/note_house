# Windows 运维命令大全

## 一、系统信息与硬件管理
| 命令         | 功能                                  | 示例                                                         |
| ------------ | ------------------------------------- | ------------------------------------------------------------ |
| `systeminfo` | 查看系统配置信息                      | `systeminfo`（显示系统详细信息）                             |
| `wmic`       | WMI命令行工具，用于获取硬件和系统信息 | `wmic os get caption,version`（获取操作系统信息）<br>`wmic cpu get name`（获取CPU信息） |
| `msinfo32`   | 打开系统信息窗口                      | 直接运行 `msinfo32`                                          |
| `tasklist`   | 查看当前运行的进程                    | `tasklist`（显示所有进程）<br>`tasklist /svc`（显示进程及其关联的服务） |

## 二、文件与目录操作
| 命令       | 功能               | 示例                                                        |
| ---------- | ------------------ | ----------------------------------------------------------- |
| `dir`      | 列出目录内容       | `dir`（显示当前目录内容）<br>`dir /s`（递归显示子目录内容） |
| `tree`     | 以树形结构显示目录 | `tree`（显示当前目录结构）<br>`tree /f`（包含文件列表）     |
| `xcopy`    | 复制目录及文件     | `xcopy C:\Source D:\Backup /s /e`（复制目录及其子目录）     |
| `robocopy` | 高级文件复制工具   | `robocopy C:\Source D:\Backup /mir`（镜像复制目录）         |

## 三、用户与权限管理
| 命令             | 功能               | 示例                                                         |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| `net user`       | 管理用户账户       | `net user`（查看用户列表）<br>`net user /add NewUser P@ssw0rd`（创建新用户） |
| `net localgroup` | 管理本地用户组     | `net localgroup Administrators`（查看管理员组成员）<br>`net localgroup Users /add NewUser`（将用户添加到用户组） |
| `icacls`         | 设置文件和目录权限 | `icacls C:\Folder /grant:r User:(F)`（授予用户完全控制权限） |

## 四、服务管理
| 命令        | 功能         | 示例                                                         |
| ----------- | ------------ | ------------------------------------------------------------ |
| `net start` | 启动服务     | `net start`（查看已启动的服务）<br>`net start "ServiceName"`（启动指定服务） |
| `net stop`  | 停止服务     | `net stop "ServiceName"`（停止指定服务）                     |
| `sc`        | 服务控制命令 | `sc query`（显示所有服务状态）<br>`sc config "ServiceName" start= auto`（设置服务为自动启动） |

## 五、性能监控与资源管理
| 命令          | 功能                  | 示例                                        |
| ------------- | --------------------- | ------------------------------------------- |
| `perfmon`     | 打开性能监视器        | 直接运行 `perfmon`                          |
| `resmon`      | 打开资源监视器        | 直接运行 `resmon`                           |
| `tasklist /m` | 查看进程占用的DLL模块 | `tasklist /m`（显示所有进程及其加载的模块） |

## 六、磁盘与存储管理
| 命令       | 功能         | 示例                                                         |
| ---------- | ------------ | ------------------------------------------------------------ |
| `diskpart` | 磁盘分区工具 | 在命令提示符中输入 `diskpart`，然后使用 `list disk`、`select disk X`、`create partition` 等命令进行磁盘操作 |
| `chkdsk`   | 检查磁盘错误 | `chkdsk C:`（检查C盘错误）<br>`chkdsk C: /f`（修复磁盘错误） |
| `defrag`   | 磁盘碎片整理 | `defrag C: /u`（显示碎片整理进度）                           |

## 七、任务调度与自动化
| 命令       | 功能                   | 示例                                                         |
| ---------- | ---------------------- | ------------------------------------------------------------ |
| `schtasks` | 创建和管理计划任务     | `schtasks /create /tn "DailyBackup" /tr "robocopy C:\Data D:\Backup /mir" /sc daily /st 02:00`（创建每天凌晨2点的备份任务） |
| `at`       | 安排任务在指定时间运行 | `at 18:00 shutdown /s`（晚上6点关机）                        |

## 八、打印与设备管理
| 命令       | 功能                         | 示例                                                         |
| ---------- | ---------------------------- | ------------------------------------------------------------ |
| `net view` | 查看网络中的打印机和其他资源 | `net view`（查看网络资源）<br>`net view \\ComputerName`（查看指定计算机的共享资源） |
| `printui`  | 打开打印机安装向导           | 直接运行 `printui`                                           |

## 九、事件查看与日志管理
| 命令       | 功能             | 示例                                                         |
| ---------- | ---------------- | ------------------------------------------------------------ |
| `eventvwr` | 打开事件查看器   | 直接运行 `eventvwr`                                          |
| `wevtutil` | 事件日志实用工具 | `wevtutil qe Application /q:"*[System[Level=2]]"`（查询应用程序日志中的错误事件） |

## 十、远程桌面与连接管理
| 命令            | 功能         | 示例                                                         |
| --------------- | ------------ | ------------------------------------------------------------ |
| `mstsc`         | 远程桌面连接 | `mstsc`（打开远程桌面连接窗口）<br>`mstsc /v:192.168.1.100`（连接到指定IP的远程计算机） |
| `query session` | 查看远程会话 | `query session`（查看当前远程会话）                          |

## 十一、系统更新与维护
| 命令      | 功能                   | 示例                                               |
| --------- | ---------------------- | -------------------------------------------------- |
| `wuauclt` | 打开Windows更新窗口    | 直接运行 `wuauclt`                                 |
| `dism`    | 部署映像服务与管理工具 | `dism /online /get-packages`（查看已安装的更新包） |

## 十二、批处理与脚本
| 命令   | 功能                     | 示例                                                         |
| ------ | ------------------------ | ------------------------------------------------------------ |
| `call` | 调用另一个批处理文件     | `call script.bat`（调用script.bat文件）                      |
| `goto` | 跳转到批处理文件中的标签 | `goto label`（跳转到指定标签）                               |
| `if`   | 条件判断                 | `if exist file.txt (echo File exists) else (echo File not found)`（判断文件是否存在） |

## 十三、环境变量管理
| 命令   | 功能                           | 示例                                                         |
| ------ | ------------------------------ | ------------------------------------------------------------ |
| `set`  | 查看和设置环境变量             | `set`（查看所有环境变量）<br>`set PATH=%PATH%;C:\NewPath`（添加新路径到PATH变量） |
| `path` | 显示或设置可执行文件的搜索路径 | `path`（显示当前路径）<br>`path C:\Windows\System32;C:\NewPath`（设置新路径） |

## 十四、系统安全与防护
| 命令             | 功能              | 示例                                                         |
| ---------------- | ----------------- | ------------------------------------------------------------ |
| `netsh firewall` | 配置Windows防火墙 | `netsh firewall set opmode disable`（关闭防火墙）<br>`netsh firewall add portopening TCP 80 80`（开放80端口） |
| `certutil`       | 证书管理工具      | `certutil -hashfile file.txt SHA256`（计算文件的SHA256哈希值） |

## 十五、实用工具
| 命令      | 功能       | 示例               |
| --------- | ---------- | ------------------ |
| `calc`    | 打开计算器 | 直接运行 `calc`    |
| `notepad` | 打开记事本 | 直接运行 `notepad` |
| `write`   | 打开写字板 | 直接运行 `write`   |

## 十六、网络性能优化与监控
| 命令         | 功能                         | 示例                                                         |
| ------------ | ---------------------------- | ------------------------------------------------------------ |
| `typeperf`   | 监控网络性能计数器           | `typeperf "\Network Interface(*)\Bytes Total/sec" -o perfmon.csv`（将网络接口的字节总数/秒数据输出到CSV文件） |
| `perfmon`    | 性能监视器                   | 添加计数器：Network Interface -> Bytes Total/sec             |
| `netstat -e` | 显示网络接口的以太网统计信息 | `netstat -e`（显示发送和接收的字节数、数据包数等）           |

## 十七、网络安全与审计
| 命令                        | 功能                                      | 示例                                                         |
| --------------------------- | ----------------------------------------- | ------------------------------------------------------------ |
| `netsh advfirewall monitor` | 监控防火墙规则的匹配情况                  | `netsh advfirewall monitor show rule name=all`（显示所有防火墙规则的匹配情况） |
| `icacls`                    | 查看和修改文件和目录的访问控制列表（ACL） | `icacls C:\Folder`（显示C:\Folder的ACL）<br>`icacls C:\Folder /grant:r User:(F)`（授予用户对C:\Folder的完全控制权限） |
| `wevtutil`                  | 事件日志实用工具                          | `wevtutil qe System /q:"*[System[Provider[@name='Tcpip']]]"`（查询系统日志中所有来自Tcpip提供程序的事件） |

## 十八、网络自动化与脚本
| 命令       | 功能               | 示例                                                         |
| ---------- | ------------------ | ------------------------------------------------------------ |
| `for /f`   | 批量处理网络信息   | `for /f "tokens=2" %i in ('arp -a') do @echo %i`（提取ARP表中的IP地址） |
| `schtasks` | 创建和管理计划任务 | `schtasks /create /tn "NetworkMonitor" /tr "ping -n 10 8.8.8.8 > ping.log" /sc daily /st 00:00`（创建一个每天午夜执行的计划任务，ping 8.8.8.8十次并将结果保存到ping.log） |

## 十九、无线网络管理
| 命令             | 功能                       | 示例                                                         |
| ---------------- | -------------------------- | ------------------------------------------------------------ |
| `netsh wlan`     | 管理无线网络连接           | `netsh wlan show networks`（显示可用的无线网络）<br>`netsh wlan connect name="MyWiFi"`（连接到名为MyWiFi的无线网络） |
| `wmic nicconfig` | 获取无线网络接口的详细信息 | `wmic nicconfig where "Description like '%Wireless%'" get SSID, SignalStrength`（显示无线网络接口的SSID和信号强度） |

## 二十、虚拟网络与云服务
| 命令                        | 功能           | 示例                                                         |
| --------------------------- | -------------- | ------------------------------------------------------------ |
| `netsh interface portproxy` | 配置端口转发   | `netsh interface portproxy add v4tov4 listenport=80 connectaddress=192.168.1.100 connectport=80`（将本地80端口的流量转发到192.168.1.100的80端口） |
| `awscli` / `azcli`          | 管理云网络资源 | `aws ec2 describe-vpcs`（列出AWS账户中的所有VPC）<br>`az network vnet list`（列出Azure订阅中的所有虚拟网络） |

## 二十一、国际化的网络命令
| 命令     | 功能                       | 示例                                                         |
| -------- | -------------------------- | ------------------------------------------------------------ |
| `locale` | 查看和设置系统的区域信息   | `locale`（显示当前区域信息）<br>`locale -a`（显示支持的区域设置） |
| `chcp`   | 更改命令提示符的字符编码页 | `chcp 65001`（设置编码为UTF-8）                              |

## 二十二、网络命令的组合使用
| 组合            | 功能                                 | 示例                                                         |
| --------------- | ------------------------------------ | ------------------------------------------------------------ |
| `|`（管道符号） | 将一个命令的输出作为另一个命令的输入 | `ping -n 10 8.8.8.8 | find "TTL="`（提取ping命令输出中包含TTL=的部分） |
| `>`和`>>`       | 将命令输出保存到文件中               | `netstat -ano > netstat.log`（将netstat的输出保存到netstat.log）<br>`ipconfig /all >> network_info.txt`（将ipconfig的输出追加到network_info.txt） |

## 二十三、网络命令的错误处理
| 命令         | 功能                                         | 示例                                                    |
| ------------ | -------------------------------------------- | ------------------------------------------------------- |
| `errorlevel` | 在批处理脚本中，根据命令的返回值进行错误处理 | `ping 8.8.8.8`<br>`if %errorlevel% neq 0 echo Ping失败` |
| `timeout`    | 在网络命令执行之间添加延迟                   | `timeout /t 30`（等待30秒）                             |

## 二十三、网络命令的可视化展示
| 命令       | 功能           | 示例                                                         |
| ---------- | -------------- | ------------------------------------------------------------ |
| `start`    | 打开图形化工具 | `start http://example.com`（在默认浏览器中打开example.com）  |
| `msconfig` | 系统配置工具   | `msconfig`（打开系统配置界面，可以查看和管理网络启动项和服务） |

## 二十四、网络命令的文档与帮助
| 命令                | 功能                     | 示例                                                |
| ------------------- | ------------------------ | --------------------------------------------------- |
| `/help`或`/?`       | 显示命令的帮助信息       | `ipconfig /?`（显示ipconfig的详细帮助）             |
| `echo %errorlevel%` | 检查上一个命令的执行状态 | `echo %errorlevel%`（在脚本中检查命令是否成功执行） |

希望这份扩展版的Windows网络命令大全能够满足你的需求，为你的网络管理和故障排查提供全面的参考。如果还有其他特定的命令或场景需要补充，欢迎随时告知！



# Windows 定时任务（计划任务）详解

## 一、基础概念
Windows 定时任务（计划任务）是 Windows 操作系统提供的一种功能，允许用户在指定的时间或条件下自动执行程序、脚本或批处理文件。它可以帮助用户自动化日常任务，提高工作效率。

## 二、使用图形界面创建定时任务
1. 按下 `Win + R` 键，输入 `taskschd.msc`，然后按回车键，打开任务计划程序。
2. 在任务计划程序窗口中，点击“创建基本任务”。
3. 按照向导的提示，输入任务名称和描述，选择触发器类型（如每天、每周、每月等），设置具体执行时间，指定要执行的操作（如启动程序、发送电子邮件等），然后完成创建。

## 三、使用命令行工具（schtasks）管理定时任务
`schtasks` 是一个功能强大的命令行工具，可以用来创建、删除、查询、修改和运行计划任务。

### 1. 创建定时任务
```cmd
schtasks /create /tn "任务名称" /tr "要执行的程序或脚本路径" /sc schedule_type [/mo modifier] [/d day] [/m month] [/st starttime] [/sd startdate] [/ed enddate] [/ru username [/rp password]]
```
- `/tn`：指定任务名称。
- `/tr`：指定要执行的程序或脚本路径。
- `/sc`：指定任务的计划类型，如 `DAILY`（每天）、`WEEKLY`（每周）、`MONTHLY`（每月）、`ONCE`（一次）等。
- `/mo`：指定计划的修饰符，例如每周执行的星期几、每月执行的具体日期等。
- `/d`：指定任务执行的星期几（与 `WEEKLY` 计划类型配合使用）。
- `/m`：指定任务执行的月份（与 `MONTHLY` 计划类型配合使用）。
- `/st`：指定任务开始时间。
- `/sd`：指定任务开始日期。
- `/ed`：指定任务结束日期。
- `/ru`：指定任务运行所使用的用户名。
- `/rp`：指定任务运行所使用的密码。

### 2. 查询定时任务
```cmd
schtasks /query
```
列出所有计划任务。

### 3. 修改定时任务
```cmd
schtasks /change /tn "任务名称" /参数 新值
```
例如，修改任务的运行时间：
```cmd
schtasks /change /tn "BackupTask" /st 23:00
```

### 4. 删除定时任务
```cmd
schtasks /delete /tn "任务名称" /f
```
`/f` 参数表示强制删除，不提示确认。

### 5. 立即运行定时任务
```cmd
schtasks /run /tn "任务名称"
```

### 6. 停止正在运行的定时任务
```cmd
schtasks /end /tn "任务名称"
```

## 四、高级功能与设置
### 1. 设置任务的优先级和权限
```cmd
schtasks /create /tn "HighPriorityTask" /tr "C:\Path\To\Script.bat" /sc daily /st 03:00 /ru SYSTEM
```
- `/ru SYSTEM`：指定任务以系统账户运行，具有较高的权限。

### 2. 设置任务的运行条件
```cmd
schtasks /create /tn "ConditionalTask" /tr "C:\Path\To\Script.bat" /sc daily /st 14:00 /ri 10 /du 1:00 /it
```
- `/ri 10`：指定任务在触发后每10分钟重复一次。
- `/du 1:00`：指定任务的最大运行时间为1小时。
- `/it`：指定任务仅在空闲时运行。

### 3. 设置任务的环境变量和工作目录
```cmd
schtasks /create /tn "EnvTask" /tr "C:\Path\To\Script.bat" /sc daily /st 08:00 /ru "DOMAIN\User" /rp "Password" /env "VAR1=Value1;VAR2=Value2" /cwd "C:\WorkingDirectory"
```
- `/env`：指定任务运行时的环境变量。
- `/cwd`：指定任务运行时的工作目录。

## 五、常见应用场景
### 1. 每日自动备份数据
```cmd
schtasks /create /sc daily /tn "DailyBackup" /tr "C:\backup\backup_script.bat" /st 02:00 /ru "BackupUser" /rp "SecurePassword"
```

### 2. 定时清理系统垃圾
```cmd
schtasks /create /sc weekly /tn "SystemCleanup" /tr "C:\cleanup\cleanup_script.bat" /d sun /st 03:00
```

### 3. 自动生成并发送报告
```cmd
schtasks /create /sc monthly /tn "MonthlyReport" /tr "C:\reports\generate_report.bat" /d 1 /st 09:00
```

## 六、常见问题与解决方法
### 1. 任务未按时运行
- 检查任务计划是否启用。
- 确保指定的脚本或程序路径正确。
- 检查任务的触发器设置是否正确。

### 2. 权限问题导致任务失败
- 使用 `/ru` 和 `/rp` 参数指定运行任务的账户及其密码。
- 确保指定的账户具有足够的权限来执行任务。

### 3. 脚本执行路径错误
- 使用完整路径指定脚本，避免任务执行失败。

### 4. `schtasks` 命令权限不足
- 在管理员权限下运行命令提示符，否则可能会出现权限不足的问题。

## 七、总结
`schtasks` 是一个功能强大的计划任务管理工具，通过它，你可以轻松实现任务的自动化操作，从而提高效率、节约时间。不论是定期备份、定时清理，还是执行复杂的自动化任务，掌握 `schtasks` 命令都将成为你管理 Windows 系统的重要技能之一。