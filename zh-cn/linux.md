- **systemctl service**

```bash
sudo systemctl start frps
sudo systemctl enable frps
sudo systemctl status frps

# centos
/lib/systemd/system/frps.service
```

- root password

`sudo passwd root`

- ssh

```
apt install openssh-server
cat /etc/ssh/sshd_config
vim /root/.ssh/authorized_keys
```

```conf
# /etc/ssh/sshd_config
Port 6001
PermitRootLogin yes
```

- ssh 通过公钥无密码登录

1. 客户端通过 ssh-keygen 生成公钥/私钥对
2. 将公钥 `id_rsa.pub` 添加到服务器的 `~/.ssh/authorized_keys` 文件
3. 更改权限

    ```bash
    chmod 700 ~/.ssh
    chmod 600 authorized_keys
    ```

- 解压文件 tar

```bash
# 解压 .tar
tar –xvf frpc.tar
# 解压 .tar.gz
tar -zxvf nginx-1.12.0.tar.gz
```

- 文件权限 

rwx = 4 + 2 + 1 = 7
```bash
chmod 777 file
chmod u=rwx,g=rwx,o=rwx file
chmod a=rwx file
```

- 更改主机名

`hostnamectl set-hostname <newhostname>`

- 查看端口号

`netstat -tunlp |grep 1`

- 安装 Ubuntu 时如果没有引导，需要把整个硬盘内分区都提前删掉，不然 Ubuntu 安装程序不会安装引导程序

- 静态 ip

```shell
ifconfig
vim /etc/netplan/01-network-manager-all.yaml
netplan apply
```

```yaml
# Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    enp2s0:
      dhcp4: no
      addresses:
        - 192.168.1.123/24
      gateway4: 192.168.1.1
      nameservers:
          addresses: [192.168.1.1, 223.5.5.5]
```
