# 服务器时间
### 查看
date: 这个命令将打印当前日期和时间。
timedatectl: 这个命令将打印系统时间和日期以及时区信息。
hwclock: 这个命令将打印硬件时间，它伴随着你的服务器 BIOS。通常情况下，它与系统时间应该相同。
```sudo hwclock --show  ```

### 时间异常纠正
- ntpdate命令：这个命令会从NTP服务器（Network Time Protocol，网络时间协议）同步服务器的时间。
```sudo ntpdate -u ntp_server_address ```
其中，ntp_server_address是您要同步的NTP服务器地址。您可以通过使用 ntpdate -q ntp_server_address 命令来测试该服务器的可用性。

- timedatectl命令：这个命令可用于手动设置系统时钟。
```sudo timedatectl set-time "yyyy-MM-dd HH:mm:ss" ```

- hwclock命令：这个命令可以设置硬件时钟。使用 -w 参数将当前的系统时钟写入硬件时钟。
``` sudo hwclock -w  ```
这个命令将会把当前的系统时间写入硬件时钟。

注意： 修改服务器时间可能会对应用程序和系统运行时产生负面影响，请谨慎操作。 如果您不确定如何操作，请联系有经验的系统管理员或运维人员。

### Linux 时区正确，如何校准时间

如果您的 Linux 系统时区设置正确，但时间不正确，可以通过下面的步骤来校准时间：

使用 timedatectl 命令检查系统时钟状态：

```$ timedatectl status ```

如果输出结果中的 “NTP synchronized” 为 “yes”，则系统已经与 NTP 服务器同步过了，否则需要进行时间同步操作。

执行 NTP 时间同步命令：

```$ sudo ntpdate pool.ntp.org ```

pool.ntp.org 是一个公共的 NTP 服务器，可以被用于时间同步。如果您想使用其他的 NTP 服务器，可以将 pool.ntp.org 替换为其他的服务器地址。执行该命令将会通过 NTP 协议与服务器同步系统时间。

将系统时钟时间写入硬件时钟：

```$ sudo hwclock -w ```

该命令将会把当前系统时钟时间写入硬件时钟，以便下次系统启动时可以从硬件时钟恢复时间。

检查时间同步是否成功：

```$ timedatectl status ```

如果输出结果中的 “NTP synchronized” 为 “yes”，则时间同步成功。

注意，如果您的系统运行在虚拟机中，可能需要使用虚拟机提供的工具来进行时间同步，例如 VMware Tools 或者 Hyper-V Integration Services。


### timedatectl 命令不存在

如果 timedatectl 命令不存在，则说明您的系统不支持 systemd 工具集，可能是一些较旧的 Linux 发行版或是嵌入式系统，并且您也无法使用 timedatectl 命令调整时间和日期。此时您可以使用其他命令和工具来校准时间，例如：

使用 date 命令来获取和设置时间和日期：

$ date     # 查看当前时间和日期 

```$ sudo date -s "2022-01-01 10:00:00"     # 设置时间和日期 ```

您可以将第二个命令中的时间和日期替换为您想设置的时间和日期。

执行 NTP 时间同步命令【推荐】：

```$ sudo ntpdate pool.ntp.org  ```
如果提示 “command not found”，可以尝试先安装 NTP 工具（例如 ntp 或 chrony）再执行该命令，并将 pool.ntp.org 替换为其他 NTP 服务器地址。

使用 hwclock 命令设置硬件时钟：

```
$ sudo hwclock -w     # 将当前系统时间写入硬件时钟

$ sudo hwclock -r     # 读取硬件时钟时间 

$ sudo hwclock -s     # 将硬件时钟时间设置为当前系统时间 
```

可以使用 hwclock -r 命令来检查硬件时钟时间是否正确。

手动挑战时间系统：

如果您无法通过以上命令准确地设置时间和日期，您可以尝试手动调整系统时间。但需要注意的是，手动调整时间可能会在一些应用程序中导致问题或错误，建议仅在紧急情况下使用这种方法。

```$ sudo date +%Y%m%d -s "20220101"     # 设置日期（年月日） 

$ sudo date +%T -s "10:00:00"     # 设置时间（时分秒） ```

您可以根据需要修改上面的时间和日期。同时，如果您的系统运行在虚拟机中，则可能还需要考虑虚拟化平台的时间设置和同步。
