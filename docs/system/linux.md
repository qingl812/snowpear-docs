# linux

## root passwd
`sudo passwd root`

## ssh
`apt install openssh-server`
`cat /etc/ssh/sshd_config`
`/root/.ssh/authorized_keys`

```conf
Port 6001
PermitRootLogin yes
```

## ssh 通过公钥无密码登录

1. 客户端通过 ssh-keygen 生成公钥/私钥对
2. 将公钥 `id_rsa.pub` 添加到服务器的 `~/.ssh/authorized_keys` 文件
3. 更改权限 `chmod 700 ~/.ssh` `chmod 600 authorized_keys`

## other

```bash
# 解压 tar 文件
tar –xvf frpc.tar
# 解压 tar.gz
tar -zxvf nginx-1.12.0.tar.gz

# npm 镜像临时设置
npm --registry https://registry.npm.taobao.org install gitbook-cli -g

# 权限
# rwx = 4 + 2 + 1 = 7
chmod 777 file  # (等价于  chmod u=rwx,g=rwx,o=rwx file 或  chmod a=rwx file)
# 更改主机名
hostnamectl set-hostname <newhostname>
# 查看端口号
netstat -tunlp |grep 1
```