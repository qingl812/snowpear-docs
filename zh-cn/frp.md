# frp

- 文档 https://gofrp.org/docs/

```shell
wget https://github.com/fatedier/frp/releases/download/v0.38.0/frp_0.38.0_linux_amd64.tar.gz
tar -zxvf frp_0.38.0_linux_amd64.tar.gz
cd frp_0.38.0_linux_amd64/
```

# frps.ini

```conf
[common]
#与客户端绑定的进行通信的端口
bind_port = 

vhost_http_port = 80
vhost_https_port = 443

# console or real logFile path like ./frps.log
log_file = ./frps.log
# trace, debug, info, warn, error
log_level = info
log_max_days = 30

dashboard_port = 
dashboard_user = 
dashboard_pwd = 

token = 
subdomain_host = 
```

# frps.service

```conf
[Unit]
Description=Frp Server Service
After=network.target

[Service]
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/bin/frps/frps -c /bin/frps/frps.ini
LimitNOFILE=1048576

[Install]
WantedBy=multi-user.target
```

# frpc.ini

```conf
[common]
server_addr =
server_port =
token =

log_file = /bin/frpc/logs/frps.log

[nginx]
type = http
local_port = 80
```

# frpc.service

```conf
[Unit]
Description=Frp Client Service
After=network.target

[Service]
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart==/bin/frpc/frpc -c /bin/frpc/frpc.ini
LimitNOFILE=1048576

[Install]
WantedBy=multi-user.target
```
