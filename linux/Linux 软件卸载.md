# nginx
```bash
# 1.停止nginx服务
systemctl stop nginx

# 2.判断安装方式
# 输出ii nginx nginx-common python3-certbot-nginx 是apt安装，没有则是其他安装方式
dpkg -l | grep nginx

# 3.删除
sudo apt-get purge nginx nginx-common python3-certbot-nginx -y

# 4.清理残余
sudo apt-get autoremove --purge -y


```