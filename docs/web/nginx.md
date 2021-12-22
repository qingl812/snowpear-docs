# build
```shell
wget $nginx_url
tar -zxvf $nginx_url
cd $nginx_url
./configure --prefix=/bin/nginx
make
make install
# 配置
vim /usr/lib/systemd/system/nginx.service
sudo systemctl daemon-reload
sudo systemctl start nginx.service
sudo systemctl enable nginx.service
rm -rf nginx/html
mkdir nginx/html
```

# nginx.conf

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
        listen       8200;
        server_name  localhost;

        location / {
            root    html/home;
            index  index.html;
        }

        location /docs {
            alias   html/docs/;
            index  index.html;
        }
    }
}
```

# nginx.servive
```conf
# nginx_root

[Unit]
Description=nginx for snowpear website github: https://github.com/qingl812/snowpear-install
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
ExecStart=$nginx_root/sbin/nginx
ExecReload=$nginx_root/sbin/nginx -s reload
ExecStop=$nginx_root/sbin/nginx -s stop

[Install]
WantedBy=multi-user.target
```

## centos nginx

```shell
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