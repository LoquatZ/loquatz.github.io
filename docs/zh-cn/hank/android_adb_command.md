## Android ADB 常用命令

### busybox
1. 查看CPU内存占用
```zsh
busybox top
```

### dumpsys
1. gfxinfo: 提供有关应用渲染性能的信息。可以用来分析应用的帧率和渲染时间，对于识别UI性能问题非常有用。
```zsh
dumpsys gfxinfo [包名]
```
2. meminfo: 显示有关系统或特定应用内存使用的信息。对于监控和优化内存使用非常有帮助。
```zsh
dumpsys meminfo [包名/进程名]
```
3. battery: 提供关于设备电池状态和使用情况的信息。对于分析应用对电池影响有重要作用。
```zsh
dumpsys battery
```
4. activity: 显示当前活动的或最近运行的应用信息。非常有用于跟踪应用的生命周期状态。
```zsh
dumpsys activity [活动/包名]
```
5. wifi: 提供有关设备 Wi-Fi 状态的详细信息，包括连接的网络、信号强度等。
```zsh
dumpsys wifi
```
6. cpuinfo: 显示CPU使用情况，有助于识别处理器占用情况和性能瓶颈。
```zsh
dumpsys cpuinfo
```
7. batterystats: 提供关于电池使用统计的详细信息，有助于分析应用对电池寿命的影响。
```zsh
dumpsys batterystats
```
8. netstats: 提供网络使用数据，包括数据使用量和连接状态。
```zsh
dumpsys netstats
```
9. alarm: 显示有关闹钟和定时任务的信息，对于调试后台任务和闹钟行为很有帮助。
```zsh
dumpsys alarm
```
10. diskstats: 提供磁盘使用和I/O统计信息，有助于分析存储性能和磁盘空间使用情况。
```zsh
dumpsys diskstats
```

### pm

1. 列出所有应用:
```zsh
pm list packages
```
2. 列出系统应用:
```zsh
pm list packages -s
```
3. 列出第三方应用:
```zsh
pm list packages -3
```
4. 列出禁用的应用:
```zsh
pm list packages -d
```
5. 清除应用数据和缓存:
```zsh
pm clear [包名]
```
6. 禁用应用:
```zsh
pm disable [包名]
```
7. 启用应用:
```zsh
pm enable [包名]
```
8. 查看应用的安装路径:
```zsh
pm path [包名]
```
### am
1. 启动 Activity:
```zsh
am start -n [包名]/[活动名]
```
2. am startservice [包名]/[服务名]
```zsh
am startservice [包名]/[服务名]
```
3. 发送广播:
```zsh
 am broadcast -a [动作] --es [键] [值]
```
4. 强制停止应用:
```zsh
m force-stop [包名]
```