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