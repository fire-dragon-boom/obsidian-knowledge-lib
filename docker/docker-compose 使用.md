# dc命令
- 启动
	```bash
	# 启动所有不带profile的容器
	docker compose up -d
	
	# 启动指定profile容器+不带profile的容器
	docker compose --profile <profile> up -d
	
	# 启动指定容器
	docker compose up -d <container's name>
	```
- 查看状态
	```bash
	docker compose ps
	```
- 停止并删除容器
	```bash
	docker compose down
	```
- 重启容器
	```bash
	docker compose restart
	```



# compose配置文件
## 添加权限
- 所有权限
	```yaml
	# 添加所有权限
	privileged: true
	```
- 添加细分权限
	```yaml
	
	cap_add: 
	 - NET_ADMIN 
	 - NET_RAW
	```














