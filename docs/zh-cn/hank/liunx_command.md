## Linux 命令记录

### systemd

- 启动服务
```bash
systemctl start 服务名称
```

-  停止服务:
```bash
systemctl stop 服务名称
```

- 重启服务
```bash
systemctl restart 服务名称
```

- 查看服务状态:
```bash
systemctl status 服务名称
```

- 使服务在启动时自动运行
```bash
systemctl enable 服务名称
```

- 禁止服务在启动时自动运行
```bash
systemctl disable 服务名称
```

- 查看systemd 运行service的日志
```bash
journalctl -f -u package
```

### lsof
```bash
lsof -i :端口号
```