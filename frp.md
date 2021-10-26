# frp 配置

```bash
scp -P 7001 'C:\frpc.tar' root@0.0.0.0:/root/frpc.tar
tar –xvf frpc.tar
# 开机启动
# conf 在最后
vim /lib/systemd/system/frps.service
vim /lib/systemd/system/frpc.service

systemctl start frps
systemctl enable frps
systemctl status frps
```

## server conf

```conf
[Unit]
Description=Frp Server Service
After=network.target

[Service]
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/myapps/frps/frps -c /myapps/frps/frps.ini
LimitNOFILE=1048576

[Install]
WantedBy=multi-user.target
```

## client conf

```conf
[Unit]
Description=Frp Client Service
After=network.target

[Service]
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/myapps/frpc/frpc -c /myapps/frpc/frpc.ini
ExecReload=/myapps/frpc/frpc reload -c /myapps/frpc/frpc.ini
LimitNOFILE=1048576

[Install]
WantedBy=multi-user.target
```
