# Linux

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
```

# windows

```bash
# 端口转发
# 添加端口转发
# listenaddress 参数可以省略
netsh interface portproxy add v4tov4 listenport=1234 listenaddress=127.0.0.1 connectport=22 connectaddress=192.168.1.1
netsh interface portproxy add v4tov4 listenport=1234 connectaddress=127.0.0.1 connectport=22 protocol=tcp
# 删除端口转发
netsh interface portproxy del v4tov4 listenport=1234 listenaddress=127.0.0.1
# 查看已存在的端口映射
netsh interface portproxy show v4tov4
netsh interface portproxy show all

# windows 向 Linux 传输文件
scp -P 1234 'C:\' root@192.168.1.1:/home/
```

# nginx

```bash
# 安装常用库，并不都是必备的库
yum install -y gcc gcc-c++ cmake make git nodejs
# 安装必备库
yum install -y pcre pcre-devel
yum install -y zlib zlib-devel
yum install -y openssl openssl-devel
# install
cd /myapps/
wget https://nginx.org/download/nginx-1.20.1.tar.gz
tar -zxvf nginx-1.12.0.tar.gz
rm nginx-1.20.1.tar.gz
cd nginx-1.20.1
./configure --prefix=/myapps/nginx
make
make install
vim /usr/lib/systemd/system/nginx.service
vim /myapps/nginx/conf/nginx.conf
```

```conf
# nginx.service
[Unit]
Description=nginx - high performance web server
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
ExecStart=/myapps/nginx/sbin/nginx
ExecReload=/myapps/nginx/sbin/nginx -s reload
ExecStop=/myapps/nginx/sbin/nginx -s stop

[Install]
WantedBy=multi-user.target
```

```conf
# nginx.conf
worker_processes  1;

error_log  logs/error.log;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;

    keepalive_timeout  65;

    server {
        listen       8102;
        server_name  localhost;

        location / {
            root   /myapps/www/qingl/docs/_book;
            index  index.html;
        }
    }
}
```

# frp

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

-   server conf

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

-   client conf

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

# docker

docker 配置 nginx

-   安装（centos8）

1. 卸载旧版

```bash
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

2. 设置仓库

```bash
sudo yum install -y yum-utils
sudo yum-config-manager \
 --add-repo \
 https://download.docker.com/linux/centos/docker-ce.repo
```

3. 下载安装 docker

```bash
sudo yum install docker-ce docker-ce-cli containerd.io
# 如提示报错，可以使用如下命令
sudo yum install docker-ce docker-ce-cli containerd.io --allowerasing
```

4. 开机启动

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

5. HelloWorld

```bash
sudo docker run hello-world
docker ps -a
docker rm 2072e0c9222c
```

6. nginx

```bash
docker pull nginx
docker run --name nginx-winterwonder -p 80:80 -d nginx
docker exec -it 6560d1561352 bash
cat /etc/nginx/nginx.conf
cat /usr/share/nginx/html/index.html
exit
```

-   其他

```bash
# 修改 docker 中一个文件
docker cp /home/test/index.html 6560d1561352://usr/share/nginx/html/index.html
# 容器保存为镜像
docker commit nginx-winterwonder wtwd-nginx-image
# 停止容器
docker stop 46af059fadd4
# 删除容器
docker rm 46af059fadd4
# 删除 image
docker rmi e7ecc581a4e4
# 容器重命名
docker rename nginx-winterwonder winterwonder
# 映射配置文件和网站静态资源
docker run --name nginxServer -p 80:80 -v /home/www/server/nginx.conf:/etc/nginx/nginx.conf -v /home/www/server/:/etc/nginx/html -d nginx
```

# gitbook

-   更新

```bash
cd /myapps/www/qingl/docs
git pull
gitbook build
```

# git

```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
# 连接到 github
# 使用 ssh-keygen 命令生成一对密钥，之后把公钥添加到 github 账户中即可
```
