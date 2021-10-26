# docker 配置 nginx

## 安装（centos8）

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

## 其他

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
