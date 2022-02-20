# ubuntu

- 安装 Ubuntu 时如果没有引导，需要把整个硬盘内分区都提前删掉，不然 Ubuntu 安装程序不会安装引导程序

## 静态 ip

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
