# docker

## HelloWorld

```bash
sudo docker run hello-world
docker ps -a
docker rm 2072e0c9222c
```

## nginx

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