# nextcloud

```shell
mkdir /SnowPear/data
sudo apt install -y docker-compose
vim docker-compose.yml
# https://github.com/nextcloud/docker#how-to-use-this-image
sudo docker-compose up -d
```

```conf
# docker-compose.yml
# Iqwa1NDGnhQDHPor 为所有密码
version: '2'

volumes:
  nextcloud:
  db:

services:
  db:
    container_name: nextcloud_db
    image: mariadb:10.5
    restart: always
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    volumes:
      - /SnowPear/data/nextcloud-db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=Iqwa1NDGnhQDHPor
      - MYSQL_PASSWORD=Iqwa1NDGnhQDHPor
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud

  app:
    container_name: nextcloud
    image: nextcloud
    restart: always
    ports:
      - 8001:80
    links:
      - db
    volumes:
      - /SnowPear/data/nextcloud-html:/var/www/html
    environment:
      - MYSQL_PASSWORD=Iqwa1NDGnhQDHPor
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_HOST=db
```
