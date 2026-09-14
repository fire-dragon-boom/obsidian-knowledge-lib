# 推荐镜像
```
其他使用方法
docker pull m.daocloud.io/docker.io/<image_name>

docker pull m.daocloud.io/docker.io/metacubex/mihomo:Alpha
docker pull metacubex/mihomo:Alpha

docker pull 1ms.run/docker.io/metacubex/mihomo:Alpha
```

```json

{
"registry-mirrors": [
		"https://docker.m.daocloud.io",
		"https://docker.1ms.run"
	]
}
```


# 修改镜像
1. 修改/etc/docker/daemon.json
	```json
	1panel镜像
	https://docker.1panel.live
	https://hub.1panel.dev
	https://docker.1ms.run	 
	{
	    "registry-mirrors": [
	        "https://registry.docker-cn.com",
	        "https://docker.mirrors.ustc.edu.cn",
	        "https://hub-mirror.c.163.com",
	        "https://mirror.baidubce.com",
	        "https://ccr.ccs.tencentyun.com"，
		   ]
	}

	```
2. 重启docker
	```bash
	sudo systemctl daemon-reload		#重启daemon进程
	sudo systemctl restart docker		#重启docker
	```
3. 验证
	```bash
	docker info
	```

# docker pull 配置代理

## service 配置文件

1. **创建 Docker 服务的配置目录**：
    ```bash
    sudo mkdir -p /etc/systemd/system/docker.service.d
    ```

2. **创建并编辑代理配置文件**：

    ```bash
    sudo nano /etc/systemd/system/docker.service.d/http-proxy.conf
    ```

3. **将以下标准配置粘贴进去**：

    ```ini
    [Service]
    Environment="HTTP_PROXY=http://127.0.0.1:7890"
    Environment="HTTPS_PROXY=http://127.0.0.1:7890"
    Environment="NO_PROXY=localhost,127.0.0.1,://docker-cn.com,://163.com"
    ```

4. **刷新系统配置并重启 Docker 服务**：

    ```bash
    sudo systemctl daemon-reload
    ```

    ```bash
    sudo systemctl restart docker
    ```

    ```bash
	sudo systemctl daemon-reload && sudo systemctl restart docker
    ```

## daemon.json 配置文件
从 Docker Engine 23.0 版本开始
1. 在 WSL 内打开或创建 `/etc/docker/daemon.json` 文件：
	```bash
	sudo nano /etc/docker/daemon.json
	```


 2. 入以下配置内容：

```json
{
  "proxies": {
    "http-proxy": "http://<宿主机IP>:<代理端口>",
    "https-proxy": "http://<宿主机IP>:<代理端口>",
    "no-proxy": "localhost,127.0.0.1"
  }

}


```

---

```json
  "proxies": {
    "http-proxy": "http://127.0.0.1:7890",
    "https-proxy": "http://127.0.0.1:7890",
    "no-proxy": "localhost,127.*,192.168.*,10.*,172.16.*,172.17.*,172.18.*,172.19.*,172.20.*,172.21.*,172.22.*,172.23.*,172.24.*,172.25.*,172.26.*,172.27.*,172.28.*,172.29.*,172.30.*,172.31.*"
  }
```